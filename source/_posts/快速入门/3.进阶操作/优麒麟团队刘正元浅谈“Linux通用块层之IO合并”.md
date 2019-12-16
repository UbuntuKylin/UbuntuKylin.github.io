---
title: 优麒麟团队刘正元浅谈“Linux通用块层之IO合并”
toc: true
date: 2019-06-24 09:02:40
tags:
categories:
---


本文作者**刘正元**，来自天津麒麟（优麒麟开发团队之一）， linux 内核爱好者，对内核 IO 子系统和内核调试工具这块比较感兴趣，向上游内核贡献过一些 patch，目前在公司负责文件 IO 协议栈的调试调优。在系统开发期间，刘正元也曾在宋宝华“ [Linux阅码场](https://mp.weixin.qq.com/s?__biz=MzAwMDUwNDgxOA==&mid=2652664651&idx=1&sn=3b908b92b4209fd49bac561814369e5a&chksm=810f35d6b678bcc0353c80e744244ab61ca81b93ae4adf18dfdff28ab35b6f97c0e7635f5f46&mpshare=1&scene=1&srcid=0605uHWZBejaZQ1PEIru1IjU#rd)”微信公众平台发表多篇文章，本文也是出自该处。

![](https://www.ubuntukylin.com/upload/201806/1528256784870902.jpg)

所谓请求合并就是将进程内或者进程间产生的在物理地址上连续的多个IO请求合并成单个IO请求一并处理，从而提升IO请求的处理效率。在前面有关通用块层介绍的系列文章当中我们或多或少地提及了IO请求合并的概念，本篇我们从头集中梳理IO请求在block layer的来龙去脉，以此来增强对IO请求合并的理解。

首先来看一张图，下面的图展示了IO请求数据由用户进程产生，到最终持久化存储到物理存储介质，其间在内核空间所经历的数据流以及IO请求合并可能的触发点。

![](https://www.ubuntukylin.com/upload/201806/1528254005961032.png)

从内核的角度而言，进程产生的IO路径主要有图中①②③所示的三条：

①　缓存IO,对应图中的路径①，系统中绝大部分IO走的这种形式，充分利用filesystem层的page cache所带来的优势， 应用程序产生的IO经系统调用落入page cache之后便可以直接返回，page cache中的缓存数据由内核回写线程在适当时机负责同步到底层的存储介质之上，当然应用程序也可以主动发起回写过程（如fsync系统调用）来确保数据尽快同步到存储介质上，从而避免系统崩溃或者掉电带来的数据不一致性。缓存IO可以带来很多好处，首先应用程序将IO丢给page cache之后就直接返回了，避免了每次IO都将整个IO协议栈走一遍，从而减少了IO的延迟。其次，page cache中的缓存最后以页或块为单位进行回写，并非应用程序向page cache中提交了几次IO,回写的时候就需要往通用块层提交几次IO,这样在提交时间上不连续但在空间上连续的小块IO请求就可以合并到同一个缓存页中一并处理。再次，如果应用程序之前产生的IO已经在page cache中，后续又产生了相同的IO，那么只需要将后到的IO覆盖page cache中的旧IO，这样一来如果应用程序频繁的操作文件的同一个位置，我们只需要向底层存储设备提交最后一次IO就可以了。最后，应用程序写入到page cache中的缓存数据可以为后续的读操作服务，读取数据的时候先搜索page cache，如果命中了则直接返回，如果没命中则从底层读取并保存到page cache中，下次再读的时候便可以从page cache中命中。

②　非缓存IO（带蓄流），对应图中的路径②，这种IO绕过文件系统层的cache。用户在打开要读写的文件的时候需要加上“O_DIRECT”标志，意为直接IO，不让文件系统的page cache介入。从用户角度而言，应用程序能直接控制的IO形式除了上面提到的“缓存IO”，剩下的IO都走的这种形式，就算文件打开时加上了”O_SYNC”标志，最终产生的IO也会进入蓄流链表（图中的Plug List）。如果应用程序在用户空间自己做了缓存，那么就可以使用这种IO方式，常见的如数据库应用。

③　非缓存IO（不带蓄流），对应图中的路径③，内核通用块层的蓄流机制只给内核空间提供了接口来控制IO请求是否蓄流，用户空间进程没有办法控制提交的IO请求进入通用块层的时候是否蓄流。严格的说用户空间直接产生的IO都会走蓄流路径，哪怕是IO的时候附上了“O_DIRECT”和”O_SYNC”标志（可以参考《Linux通用块层介绍（part1: bio层）》中的蓄流章节），用户间接产生的IO，如文件系统日志数据、元数据，有的不会走蓄流路径而是直接进入调度队列尽快得到调度。注意一点，通用块层的蓄流只提供机制和接口而不提供策略，至于需不需要蓄流、何时蓄流完全由内核中的IO派发者决定。

应用程序不管使用图中哪条IO路径，内核都会想方设法对IO进行合并。内核为促进这种合并，在IO协议栈上设置了三个最佳狙击点：

 * Cache（页高速缓存）

 * Plug List（蓄流链表）

 * Elevator Queue（调度队列）

### cache 合并

IO处在文件系统层的page cache中时只有IO数据，还没有IO请求（bio或request）,只有page cache在读写的时候才会产生IO请求。本文主要介绍IO请求在通用块层的合并，因此对于IO在cache层的合并只做现象分析，不深入到内部逻辑和代码细节。

如果是缓存IO,用户进程提交的写数据会积聚在page cache中。cache保存IO数据的基本单位为page,大小一般为4K,因此cache又叫“页高速缓存”， 用户进程提交的小块数据可以缓存到cache中的同一个page中，最后回写线程将一个page中的数据一次性提交给通用块层处理。以dd程序写一个裸设备为例，每次写1K数据，连续写16次：

　　dd if=/dev/zero of=/dev/sdb bs=1k count=16

通过blktrace观测的结果为：

　　blktrace -d /dev/sdb -o - | blkparse -i -

![](https://www.ubuntukylin.com/upload/201806/1528254017439804.png)

bio请求在通用块层的处理情况主要是通过第六列反映出来的，如果对blkparse的输出不太了解，可以man一下blktrace。对照每一行的输出来看看应用程序产生的写IO经由page cache之后是如何派发到通用块层的：

![](https://www.ubuntukylin.com/upload/201806/1528254026772374.png)

现阶段只关注IO是如何从page cache中派发到通用块层的，所以后面的泻流、派发过程没有贴出来。回写线程–kworker以8个扇区（扇区大小为512B, 8个扇区为4K对应一个page大小）为单位将dd程序读写的1K数据块派发给通用块层处理。dd程序写了16次，回写线程只写了4次（对应四次Q），page cache的缓存功能有效的合并了应用程序直接产生的IO数据。

文件系统层的page cache对读IO也有一定的作用，带缓存的读IO会触发文件系统层的预读机制，所谓预读有专门的预读算法，通过判断用户进程IO趋势，提前将存储介质上的数据块读入page cache中，下次读操作来时可以直接从page cache中命中，而不需要每次都发起对块设备的读请求。还是以dd程序读一个裸设备为例，每次读1K数据，连续读16次：

　　dd if=/dev/sdb of=/dev/zero bs=1K count=16

通过blktrace观测的结果为：

　　blktrace -d /dev/sdb -o - | blkparse -i -

![](https://www.ubuntukylin.com/upload/201806/1528254037273702.png)

同样只关注IO是如何从上层派发到通用块层的，不关注IO在通用块层的具体情况，先不考虑P，I，U，D，C等操作，那么上面的输出可以简单解析为：

![](https://www.ubuntukylin.com/upload/201806/1528254048278725.png)

读操作是同步的，所以触发读请求的是dd进程本身。dd进程发起了16次读操作，总共读取16K数据，但是预读机制只向底层发送了两次读请求，分别为0+32(16K), 32+64(32K)，总共预读了16 + 32 = 48K数据，并保存到cache中，多预读的数据可以为后续的读操作服务。

### plug 合并

linuxer公众号中介绍bio和request的系列文章，熟悉IO请求在通用块层的处理，以及蓄流(plug)机制的原理和接口。特别推荐宋宝华老师写的《文件读写（BIO）波澜壮阔的一生》，通俗易懂地介绍了一个文件io的生命周期。

每个进程都有一个私有的蓄流链表，进程在往通用块层派发IO之前如果开启了蓄流功能，那么IO请求在被发送给IO调度器之前都保存在蓄流链表中，直到泄流(unplug)的时候才批量交给调度器。蓄流的主要目的就是为了增加请求合并的机会，bio在进入蓄流链表之前会尝试与蓄流链表中保存的request进行合并,使用的接口为blk_attempt_plug_merge().本文是基于内核4.17分析的，源码来源于4.17-rc1。

blk_attempt_plug_merge:
    list_for_each_entry_reverse(rq, plug_list, queuelist) {
                ......
                switch (blk_try_merge(rq, bio)) {
                case ELEVATOR_BACK_MERGE:
                        merged = bio_attempt_back_merge(q, rq, bio);
                        break;
                case ELEVATOR_FRONT_MERGE:
                        merged = bio_attempt_front_merge(q, rq, bio);
                        break;
                case ELEVATOR_DISCARD_MERGE:
                        merged = bio_attempt_discard_merge(q, rq, bio);
                        break;
                default:
                        break;
                }
    }

代码遍历蓄流链表中的request，使用blk_try_merge找到一个能与bio合并的request并判断合并类型，蓄流链表中的合并类型有三种：ELEVATOR_BACK_MERGE，ELEVATOR_FRONT_MERGE，ELEVATOR_DISCARD_MERGE。普通文件IO操作只会进行前两种合并，第三种是丢弃操作的合并，不是普通的IO的合并，故不讨论。

### bio后向合并 (ELEVATOR_BACK_MERGE)

为了验证IO请求在通用块层的各种合并形式，准备了以下测试程序，该测试程序使用内核原生支持的异步IO引擎，可异步地向内核一次提交多个IO请求。为了减少page cache和文件系统的干扰，使用O_DIRECT的方式直接向裸设备派发IO。

iotc.c
...
/* dispatch 3 4k-size ios using the io_type specified by user */
＃define NUM_EVENTS 3
＃define ALIGN_SIZE 4096
＃define WR_SIZE 4096
enum io_type {
SEQUENCE_IO,/* dispatch 3 ios: 0-4k(0+8), 4-8k(8+8), 8-12k(16+8) */
REVERSE_IO,/* dispatch 3 ios: 8-12k(16+8), 4-8k(8+8),0-4k(0+8) */
INTERLEAVE_IO, /* dispatch 3 ios: 8-12k(16+8), 0-4k(0+8),4-8k(8+8) */ ,
IO_TYPE_END
};
int io_units[IO_TYPE_END][NUM_EVENTS] = {
{0, 1, 2},/* corresponding to SEQUENCE_IO */
{2, 1, 0},/* corresponding to REVERSE_IO */
{2, 0, 1}/* corresponding to INTERLEAVE_IO */
};
char *io_opt = "srid:";/* acceptable options */
int main(int argc, char *argv[])
{
intfd;
io_context_t ctx;
struct timespec tms;
struct io_event events[NUM_EVENTS];
struct iocb iocbs[NUM_EVENTS],
*iocbp[NUM_EVENTS];
int i, io_flag = -1;;
void *buf;
bool hit = false;
char *dev = NULL, opt;
/* io_flag and dev got set according the options passed by user , don’t paste the code of parsing here to shrink space */
fd = open(dev, O_RDWR | __O_DIRECT);
/* we can dispatch 32 IOs at 1 systemcall */
ctx = 0;
io_setup(32, &ctx);
posix_memalign(&buf,ALIGN_SIZE,WR_SIZE);
/* prepare IO request according to io_type */
for (i = 0; i < NUM_EVENTS; iocbp[i] = iocbs + i, ++i)
io_prep_pwrite(&iocbs[i], fd, buf, WR_SIZE, io_units[io_flag][i] * WR_SIZE);
/* submit IOs using io_submit systemcall */
io_submit(ctx, NUM_EVENTS, iocbp);
/* get the IO result with a timeout of 1S*/
tms.tv_sec = 1;
tms.tv_nsec = 0;
io_getevents(ctx, 1, NUM_EVENTS, events, &tms);
return 0;
}

测试程序接收两个参数，第一个为作用的设备，第二个为IO类型，定义了三种IO类型：SEQUENCE_IO（顺序），REVERSE_IO（逆序），INTERLEAVE_IO（交替）分别用来验证蓄流阶段的bio后向合并、前向合并和泄流阶段的request合并。为了减少篇幅，此处贴出的源码删除了选项解析和容错处理，只保留主干，原版位于：[点击此处](https://github.com/liuzhengyuan/iotc)。

为验证bio在蓄流阶段的后向合并，用上面的测试程序iotc顺序派发三个写io:

＃ ./iotc-d/dev/sdb-s

-d指定作用的设备sdb，-s指定IO方式为SEQUENCE_IO（顺序），表示顺序发起三个写请求：bio0(0 + 8), bio1(8 + 8), bio2(16 + 8)。通过blktrace来观察iotc派发的bio请求在通用块层蓄流链表中的合并情况：

blktrace -d /dev/sdb -o - | blkparse -i -

![](https://www.ubuntukylin.com/upload/201806/1528254084160608.png)

上面的输出可以简单解析为：

![](https://www.ubuntukylin.com/upload/201806/1528254095647471.png)

第一个bio(bio0)进入通用块层时，此时蓄流链表为空，于是申请一个request并用bio0初始化，再将request添加进蓄流链表，同时告诉blktrace蓄流已正式工作。第二个bio(bio1)到来的时候会走blk_attempt_plug_merge的逻辑，尝试调用bio_attempt_back_merge与蓄流链表中的request合并，发现正好能合并到第一个bio所在的request尾部，于是直接返回。第三个bio(bio2)的处理与第二个同理。通过蓄流合并之后，三个IO请求最终合并成了一个request(0 + 24)。用一副图来展示整个合并过程：

![](https://www.ubuntukylin.com/upload/201806/1528254105303637.png)

### bio前向合并 (ELEVATOR_FRONT_MERGE)

为验证bio在蓄流阶段的前向合并，使用iotc逆序派发三个写io:

＃ ./iotc-d/dev/sdb-r

-r指定IO方式为REVERSE_IO（逆序），表示逆序发起三个写请求：bio0(16 + 8),bio1(8 + 8), bio2(0 + 8)。blktrace的观察结果为：

blktrace -d /dev/sdb -o - | blkparse -i -

![](https://www.ubuntukylin.com/upload/201806/1528254118631038.png)

上面的输出可以简单解析为：

![](https://www.ubuntukylin.com/upload/201806/1528254143306219.png)

与前面的后向合并相比，唯一的区别是合并方式由之前的”M”变成了现在的”F”，即在blk_attempt_plug_merge中走的是bio_attempt_front_merge分支。通过下面的图来展示前向合并过程：

![](https://www.ubuntukylin.com/upload/201806/1528254164616153.png)

“plug合并”不会做request与request的进阶合并，蓄流链表中的request之间的合并会在泄流的时候做，即在下面介绍的“elevator合并”中做。

### elevator 合并

上面讲到的蓄流链表合并是为进程内的IO请求服务的，每个进程只往自己的蓄流链表中提交IO请求，进程间的蓄流链表相互独立，互不干涉。但是，多个进程可以同时对一个设备发起IO请求，那么通用块层还需要提供一个节点，让进程间的IO请求有机会进行合并。一个块设备有且仅有一个请求队列（调度队列），所有对块设备的IO请求都需要经过这个公共节点，因此调度队列（Elevator Queue）是IO请求合并的另一个节点。

先回顾一下通用块层处理IO请求的核心函数：blk_queue_bio(),上层派发的bio请求都会流经该函数，或将bio蓄流到Plug List，或将bio合并到Elevator Queue,或将bio生成request直接插入到Elevator Queue。blk_queue_bio()的主要处理流程为：

![](https://www.ubuntukylin.com/upload/201806/1528254202385663.png)

其中”A”标识的“合并到蓄流链表的request中”就是上一章介绍的“plug合并”。bio如果不能合并到蓄流链表中接下来会尝试合并到“B”标识的”合并到调度队列的request中”。”合并到调度队列的request中”只是“elevator合并”的第一个点。你可能已经发现了blk_queue_bio()将bio合并到蓄流链表或者将request添加进蓄流链表之后就没管了，从路径①可以发现蓄流链表中的request最终都是要交给电梯调度队列的，这正是”elevator合并”的第二个点，关于泄流的时机请参考我之前写的《Linux通用块层介绍（part1: bio层）》。下面分别介绍这两个合并点：

### bio合并到elevator

先看B表示的代码段：

blk_queue_bio:
switch (elv_merge(q, &req, bio)) {
case ELEVATOR_BACK_MERGE:
if (!bio_attempt_back_merge(q, req, bio))
break;
elv_bio_merged(q, req, bio);
free = attempt_back_merge(q, req);
if (free)
__blk_put_request(q, free);
else
elv_merged_request(q, req, ELEVATOR_BACK_MERGE);
goto out_unlock;
case ELEVATOR_FRONT_MERGE:
if (!bio_attempt_front_merge(q, req, bio))
break;
elv_bio_merged(q, req, bio);
free = attempt_front_merge(q, req);
if (free)
__blk_put_request(q, free);
else
elv_merged_request(q, req, ELEVATOR_FRONT_MERGE);
goto out_unlock;
default:
break;
}

合并逻辑基本与”plug合并”相似，先调用elv_merge接口判断合并类型，然后根据是后向合并或是前向合并分别调用bio_attempt_back_merge和bio_attempt_front_merge进行合并操作，由于操作对象从蓄流链表变成了电梯调度队列，bio合并完了之后还需额外干几件事：

1. 调用elv_bio_merged,该函数会调用电梯调度器注册的elevator_bio_merged_fn接口来通知调度器做相应的处理，对于deadline调度器而言该接口为NULL。

2.寻找进阶合并，参考我之前写的《Linux通用块层介绍（part2: request层）》中对进阶合并的描述，如果bio产生了后向合并，则调用attempt_back_merge试图进行后向进阶合并，如果bio产生了前向合并，则调用attempt_front_merge企图进行前向进阶合并。deadline的进阶合并接口为deadline_merged_requests， 被合并的request会从调度队列中删除。通过下面的图示来展示后向进阶合并过程，前向进阶合并同理。

![](https://www.ubuntukylin.com/upload/201806/1528254236803650.png)

3. 如果产生了进阶合并，则被合并的request可以释放了，参考上图，可调用blk_put_request进行回收。如果只产生了bio合并，合并后的request的长度和扇区地址都会发生变化，需要调用elv_merged_request->elevator_merged_fn来更新合并后的请求在调度队列的位置。deadline对应的接口为deadline_merged_request，其相应的操作为将合并的request先从调度队列移出再重新插进去。

“bio合并到elevator”的合并形式只会发生在进程间，即只有一个进程在IO的时候不会产生这种合并形式，原因在于进程在向调度队列派发IO请求或者试图与将bio与调度队列中的请求合并的时候是持有设备的队列锁得，其他进程是不能往调度队列派发请求，这也是通用块层单队列通道窄需要发展多队列的主要原因之一，只有进程在将调度队列中的request逐个派发给驱动层的时候才会将设备队列锁重新打开，即只有当一个进程在将调度队列中request派发给驱动的时候其他进程才有机会将bio合并到还未派发完的request中。所以想通过简单的IO测试程序来捕捉这种形式的合并比较困难，这对两个IO进程的IO产生时序有非常高的要求，故不演示。有兴趣的可以参考上面的github仓库，里面有patch对内核特定的请求派发位置加上延时来改变IO请求本来的时序，从而让测试程序人为的达到这种碰撞效果。

request在泄流的时候合并到elevator

通用块层的泄流接口为：blk_flush_plug_list()， 该接口主要的处理逻辑如下图所示

![](https://www.ubuntukylin.com/upload/201806/1528254245597629.png)

其中请求合并发生的点在__elv_add_request()。blk_flush_plug_list会遍历蓄流链表中的每个request，然后将每个request通过_elv_add_request接口添加到调度队列中，添加的过程中会尝试与调度队列中已有的request进行合并。

__elv_add_request:
case ELEVATOR_INSERT_SORT_MERGE:
/*
* If we succeed in merging this request with one in the
* queue already, we are done - rq has now been freed,
* so no need to do anything further.
*/
if (elv_attempt_insert_merge(q, rq))
break;
/* fall through */
case ELEVATOR_INSERT_SORT:
BUG_ON(blk_rq_is_passthrough(rq));
rq->rq_flags |= RQF_SORTED;
q->nr_sorted++;
if (rq_mergeable(rq)) {
elv_rqhash_add(q, rq);
if (!q->last_merge)
q->last_merge = rq;
}
q->elevator->type->ops.sq.elevator_add_req_fn(q, rq);
break;

泄流时走的是ELEVATOR_INSERT_SORT_MERGE分支，正如注释所说的先让蓄流的request调用elv_attempt_insert_merge尝试与调度队列中的request合并，如果不能合并则落入到ELEVATOR_INSERT_SORT分支，该分支直接调用电梯调度器注册的elevator_add_req_fn接口将新来的request插入到调度队列合适的位置。其中elv_rqhash_add是将新加入到调度队列的request做hash索引，这样做的好处是加快从调度队列寻找可合并的request的索引速度。

在泄流的时候调度队列中既有其他进程产生的request，也有当前进程从蓄流链表中派发的request（blk_flush_plug_list是先将所有request派发到调度队列再一次性queue_unplugged，而不是派发一个request就queue_unplugged）。所以“request在泄流的时候合并到elevator”既是进程内的，也可以是进程间的。

elv_attempt_insert_merge的实现只做request间的后向合并，即只会将一个request合并到调度队列中的request的尾部。这对于单进程IO而言足够了，因为blk_flush_plug_list在泄流的时候已经将蓄流链表中的request进行了list_sort（按扇区排序）。笔者曾经提交过促进进程间request的前向合并的patch（见github），但没被接收，maintainer–Jens的解析是这种IO场景很难发生，如果产生这种IO场景基本是应用程序设计不合理。通过增加时间和空间来优化一个并不常见的场景并不可取。

最后通过一个例子来验证进程内“request在泄流的时候合并到elevator”，进程间的合并同样对请求派发时序有很强的要求，在此不演示，github中有相应的测试patch和测试方法。iotc使用下面的方式派发三个写io:

＃ ./iotc-d/dev/sdb-i

-i指定IO方式为INTERLEAVE_IO（交替），表示按扇区交替的方式发起三个写请求：bio0(16 + 8),bio1(8 + 8), bio2(0 + 8)。blktrace的观察结果为：

blktrace -d /dev/sdb -o - | blkparse -i -

![](https://www.ubuntukylin.com/upload/201806/1528254255647107.png)

上面的输出可以简单解析为：

![](https://www.ubuntukylin.com/upload/201806/1528254265486421.png)

bio0(16 + 8)先到达plug list，bio1(0+8)到达时发现不能与plug list中的request合并，于是申请一个request添加到plug list。bio2(8+8)到达时首先与bio1进行后向合并。之后进程触发泄流，泄流接口函数会将plug list中的request排序，因此request(0+16)先派发到调度队列，此时调度队列为空不能进行合并。然后派发request(16+8),派发时调用elv_attempt_insert_merge接口尝试与调度队列中的其他request进行合并，发现可以与request(0+16)进行后向合并，于是两个request合并成一个，最后向设备驱动派发的只有一个request(0+24)。整个过程可以用下面的图来展示：

![](https://www.ubuntukylin.com/upload/201806/1528254276774034.png)

### 小结

通过cache、plug和elevator自上而下的三层狙击，应用程序产生的IO能最大限度的进行合并，从而提升IO带宽，降低IO延迟，延长设备寿命。page cache打头阵，既做数据缓存又做IO合并，主要是针对小块IO进行合并，因为使用内存页做缓存，所以合并后的最大IO单元为页大小，当然对于大块IO,page cache也会将它拆分成以页为单位下发，这不影响最终的效果，因为后面还有plug和elevator补刀。plug list竭尽全力合并进程内产生的IO,从设备的角度而言进程内产生的IO相关性更强，合并的可能性更大，plug list设计位于elevator queue之上而且又是每个进程私有的，因此plug list既有利于IO合并，又减轻了elevator queue的负担。elevator queue更多的是承担进程间IO的合并，用来弥补plug list对进程间合并的不足，如果是带缓存的IO，这种IO合并基本上不会出现。从实际应用角度出发，IO合并更多的是发生在page cache和plug list中。
