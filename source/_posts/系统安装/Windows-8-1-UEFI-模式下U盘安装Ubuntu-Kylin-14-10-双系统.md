---
title: 'Windows 8.1, UEFI 模式下U盘安装Ubuntu Kylin 14.10 双系统'
toc: true
date: 2019-06-24 14:30:40
tags:
categories:
---





## Windows 8.1, UEFI 模式下U盘安装Ubuntu Kylin 14.10 双系统

因办公需要，Linux 系统是必需的，本文作者是 Windows8.1 系统，笔记本电脑型号是联想 Y400。 由于虚拟机的慢速，所以决定删除一个硬盘然后独立安装 Linux 的操作系统。


### 1. Window 8.1 的情况：  
windows 8.1 系统原装正版，电脑是联想 Y400，进入 Bios（开机出现Logo后按F2），因为UEFI的引导形式，BIOS里面没有U盘启动的选项。只有 UEFI 模式和 Legacy (传统模式)这两个选项。第一个尝试是在 Legacy 模式下进行传统的安装，这个和常规的安装方式没有什么区别。这里以 Ubuntu Kylin 为例。
    准备工作：
   （1） 第一次安装的是32位 Ubuntu Kylin 14.10，安装方式是U盘安装，因为 Bios 没有从 U 盘引导的选项，所以需要做一些准备工作;
   （2） 进入Windows系统，关掉快速启动，（控制面板->电源选项->左侧选择电源按钮的功能->单击选择当前不可用的设置->在下面的关机设置中关掉快速启动）;
   （3） 开机F2（不同机器不一样），进入Bios，关掉Secure Boot（安全启动），设置UEFI模式为Legacy模式，设置Legacy优先;
   （4） U 盘格式化，最好格式化成 FAT32 格式的，然后用刻录工具刻盘，比如软通碟（作者第一次用软通碟但是刻录的 U 盘无法正确引导安装，上网查了似乎对 legacy 等支持不好，所以在网上的建议下用了 Win32DiskImager ）就没有问题;
   （5） 备份重要的文件，防止安装出问题把系统搞坏了;
   （6） 下载 MBRFIX 工具，这个是你要删除 Ubuntu Kylin 时候防止 MBR 破话 Windows 的引导导致不能进入系统;
   （7） 防患于为然，最好有个PE系统恢复盘。
   （8） 下载 DiskGenius ，这个是因为你的 U 盘做完引导盘后你如果格式化，U 盘只有几百K的容量，你需要用这个软件把 U 盘丢失为分配的内存重新分配上；

### 2. Ubuntu Kylin 14.10 Legacy U盘安装：  
这个实际上是传统安装方式;
   （1） 插入U盘，因为之前已经在 Bios 中设置过 Legacy 和 Legacy 优先了，所以正常情况下应该是可以看到一个安装画面的，这个安装画面是紫色的，下面有个小人和一个图标，看到这个画面说明是传统的安装方式，这里安装的是32位的;
   （2） 一路默认就可以了，但是比较重要的是分区这块儿;
   （3） 这里分了 swap 交换分区 -2G ，根目录 -70G ，home-120G ，这个其实没那么严格，大家可以参考网上的一些建议，注意这里没有分 boot 分区，因为默认是会将 boot 挂载在全盘上的，所以出来的结果是以 Ubuntu Kylin 引导的（其实实际上不是，后面在详细分析）;
   （4） 分区下面的启动加载就保持不变了，默认为全盘;
   （5） 好了，一路耐心等待，重启的时候（U盘要拔掉，要不有进入安装界面了），就会看到 Ubuntu Kylin 的选择界面了，可以选 Ubuntu Kylin ，也可以选 Windows 8.1,正常情况下 Ubuntu Kylin 可以进去没有问题，但是 Windows 8.1却进不去了;
   （6） 原因是因为 Windows8.1是以UEFI模式安装引导的，而 Ubuntu Kylin 是在传统模式下安装的，所以理论上在前面的安装过程中希望通过 Ubuntu Kylin 引导 Windows，但结果是俩者不协同，导致 Ubuntu Kylin 生成的 windows 启动项是错误的;
   （7） 于是问题就来了，怎么进入 windows，很简单，重启进入 Bios，把 Legacy 改回为 UEFI，然后就又可以顺利的进入 Windows 8 了，但这时候没有 Ubuntu Kylin 的进入选项，这意味着你要想进入 Ubuntu Kylin ，就重新把 Legacy 改回为 UEFI 就可以了;如果你能忍受这样的麻烦，到 这里也算是顺利完成了;
   （8） 曾经试图想把 Ubuntu Kylin 的 boot 挂载在另外的分区上，然后设置启动项为该分区，然后希望通过 easyBCD 编辑从 Windows 引导，但是根本行不通，因为 UEFI 和 Legacy 两者各自独立，很难完成互相引导，至少我没有办到;
   （9） 最后的结果就是，看似是双系统，但是每次进入不同的系统都要重新设置 Bios ，非常麻烦！

### 3. Ubuntu Kylin 14.10 UEFI U盘安装：  
因为上面不爽，一气之下在Win8下面把 Ubuntu Kylin 的盘全删了，但是手贱造成的结果就是再次试图通过设置Bios为 Legacy 然后U盘安装盘无法引 导，这是因为之前将boot挂在全盘，破坏了MBR启动项，导致系统引导出错，但我还是可以通过更改为UEFI进入win8,所以我觉得也是有一点好的， 两种模式即便传统安装的 Ubuntu Kylin 死掉了，我还是能进入win8系统，于是在win8下重新把MBR用MBRFIX工具修复一下就好了，这个工具就只用 在命令行输入一行命令就可以了;觉得这个不是办法，决定用UEFI模式安装 Ubuntu Kylin 。
   （1） U 盘格式化，只有几百K,用 DiskGenius 把U盘的这几百K删了然后把所有未分配的U盘内存重新分配;
   （2） 注意U盘要格式化为fat32的;
   （3） 下载 Ubuntu Kylin 14.10 一定要是64位的，32位什么情况我就不得知了，我的电脑是64位，这里之针对64位安装的童鞋;
   （4） 刻录U盘，插入U盘重启;
   （5） 进入 BIOS，设置为 UEFI 模式，你会看到有一个 USB 的启动选项，这是因为U盘里有 .efi 这个文件，所以UEFI模式会自动检测，选择改选项优先启动就可以了;
   （6） 重启，Ubuntu Kylin 进入安装界面，这个界面与传统安装有所不同，没有之前的小人和图标了，而是在左上角有三行字，第一行是“Install...”，选择安装就可以了;
   （7） 在分配硬盘的时候，我分了四个区 /boot 挂载为 EFI 分区（这里我分了200M），/swap 交换分区，/根目录，/home 家分区;
   （8） 下面的启动分区设置为 /boot 所在的分区;
   （9） 其实这里你看似分了一个 /boot，以为启动项会挂载到你的这个 /boot 分区上，其实不然，无论有没有这个分区，Ubuntu 都会把 EFI 文件拷贝到一 个专门的EFI启动分区，这个分区是和 WIndow8 共用的，在硬盘设置你列表中你可以明显看到，一般在 Windows OS 分区的前面，sda2，你可以仔细检查一下，因为很明显有标志;
   （10） 所以第7步中你也可以不要 /boot，而在下面把启动加载的硬盘设置为 EFI 分区就可以了;
   （11） 你可能担心这样会破坏 windows 的引导，或者你以后删除 Ubuntu Kylin 会对 windows 的引导造成问题，其实不然，这样更安全，因为这样安装会在EFI分区新建一个 Ubuntu Kylin 的efi文件夹，专门负责 ubuntu Kylin 的引导，windows 的文件夹专门负责 windows 的引导，所以删除一个另一个也不会出问题，只是删除了后会有启动项的残留项，随便用efi工具清理一下就可以了;
  （12） 继续，重启，进入 Bios ，这个会发现多了 Ubuntu Kylin 这一个条目，原来只有( windows boot manager，boot from IPv4，boot from IPv6 )，把 Ubuntu Kylin 的选项调整到最上面，这样每次开机的的时候就会有 Ubuntu Kylin 还有 Ubuntu Kylin 的修复模式还有 Windows 8;  
  目前支持 EFI 安装的 linux 系统有 Ubuntu、Ubuntu Kylin、Fedora 和 opensuse，比较新的版本支持，64位刻成盘Fat32格式基本上可以被自动检测到，安全启动要在bios里面关闭到，opensuse 支持安全启动模式下的安装，不过不知道效果怎么样，没有试验。大家在安装系统之前最好把准备工作做足，免得系统崩溃又没有PE修复盘欲哭无泪，装系统也是考验人品和耐心的事情，假如 Linux 里面可以看到 Windows 的盘符和其他硬盘，不要乱删。

原文：http://forum.ubuntu.org.cn/viewtopic.php?t=466297