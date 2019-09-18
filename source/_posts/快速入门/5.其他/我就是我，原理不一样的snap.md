---
title: 我就是我，原理不一样的snap
toc: true
date: 2019-06-24 09:03:40
tags:
categories:
---



**引言**

snap和flatpak都是新一代跨Linux发行版的软件包管理技术，上一篇我们简单介绍了flatpak的原理（传送门），今天我们接着简要介绍snap的安全机制。

 
### 简介

snap是Canoncial公司提出的新一代linux包管理工具，致力于将所有linux发行版上的包格式统一，做到“一次打包，到处使用”。目前snap已经可以在包括Ubuntu、Fedora、Mint等多个Linux发行版上使用。首先我们来了解下snap相关的各种名词：
#### snap

新一代跨Linux发行版的软件包管理技术，支持各大主流Linux发行版，通过Linux内核安全机制保证用户数据安全，彻底解决包依赖关系相关问题，并大大简化应用软件的打包工序。snap同时为安装及管理snap包的命令行工具。
#### snapd

管理snap软件包的后台服务。
#### kernel snap

使用snap格式打包的内核，包含内核镜像及内核模块。
#### OS snap

使用snap格式重新打包的rootfs，包含了运行和管理snap的基本资源，当你第一次安装snap时，OS snap 首先被安装。

#### snapcraft

将软件打包成snap格式的打包工具集。

#### snappy

原指完全基于snap构建的系统，此名称已弃用，现统一称为Ubuntu Core，即Ubuntu的全snap操作系统，有别于传统基于deb包的classic Ubuntu。

 
### 安全策略

snap应用以沙箱的方式运行。系统通过一些机制限制应用访问资源的权限来实现其安全特性，比如通过对内核安全机制AppArmor，Seccomp等的配置实现的沙箱和snap文件系统等。开发者不必过多了解系统安全机制的细节。下面简要说明snap使用的部分安全策略。
#### Sandbox

Linux Sandbox 是根据内核中支持的一些安全机制实现的进程访问控制方式。通常通过为进程分配随机uid，将进程置于chroot环境和为进程uid配置Capability等方式将进程置于严格受限的一种状态下。snap应用使用这种方式运行在系统为其分配的沙箱环境中。
#### security policy ID

每一个snap应用程序命令都有唯一的security policy ID，系统将此ID与命令绑定，由此可以为同一snap包内的不同程序配置不同的安全策略。作为系统识别命令的标示，当程序安装和运行时，系统会根据其Security Policy ID为其分配资源。在沙箱中运行的snap应用之间的通信控制也通过此ID来进行配置。 
snap应用的security policy ID的命名规则为snap.name.command 
例如，hello程序的security policy ID即为snap.hello.hello
#### snap文件系统

snap文件系统被划分为具有只读和读写两种不同权限的区域，每个snap应用有其独有的受限文件目录，如下图所示：

![](http://www.ubuntukylin.com/upload/201708/1501752729610536.png)


可以通过如下方式查看某应用的文件访问权限：

$ snap install hello
hello 2.10 from 'canonical' installed
$ snap run --shell hello.hello


$ env | grep SNAP
SNAP_USER_COMMON=/home/kylin/snap/hello/common
＃ 单用户所有版本应用的可写目录
SNAP_LIBRARY_PATH=/var/lib/snapd/lib/gl:/var/lib/snapd/void
＃ 增加到LD_LABRARY_PATH的目录
SNAP_COMMON=/var/snap/hello/common
＃ 所有用户所有版本应用的可写目录
SNAP_USER_DATA=/home/kylin/snap/hello/20
＃ 单用户指定版本应用的可写目录
SNAP_DATA=/var/snap/hello/20
＃ 所有用户指定版本应用的可写目录

由此可见，一个snap应用具有写权限的目录是极其有限的，并且每个snap应用都有其独立的可写目录。snap文件系统对snap应用相关目录的权限配置说明，这种方式实现了应用与应用，应用与系统之间的隔离。 
同时这种方式对snap应用的升级和回滚提供了很好的支持，升级时只需将确定版本的相关目录复制到更高版本的对应目录，而回退只需删除更高版本的目录。
#### AppArmor

AppArmor是一个强制访问控制系统，在内核层面对进程可访问的资源进行控制。 在snap应用程序安装时，系统会为其中的每一个命令生成其特有的AppArmor配置文件。内核对可执行程序的Capability限制也可以通过Aparmor来配置。当执行应用程序中的命令时，AppArmor机制可保证此命令不会越权访问。 作为一种内核中的安全机制，在ubuntu classic系统中也同时支持AppArmor提供的机制。但与classic系统不同，snap系统对程序的访问控制更加严格，基本做到“只满足程序执行所需的最小权限”。
#### Seccomp

Seccomp是一个内核接口访问过滤器，snap应用程序通过其独有的过滤器访问内核接口。在snap应用程序启动之前会自动配置过滤器。Seccomp在snap系统中的作用类似于AppArmor。都是控制应用程序对系统资源的访问。

Snap接口调用

snap应用被严格限制在上面介绍的安全策略下，但snap应用之间也需要进行通信，比如硬件驱动作为一个snap应用肯定要为使用这个硬件的应用提供接口和服务。下面就简单说明一下snap应用之间的通信机制。
#### 默认安全策略

在没有特殊配置时，snap应用使用默认的安全策略，其中包含之前提到的snap文件系统中的默认目录访问控制以及以下部分策略：

· snap应用安装目录的只读权限。

· 共享内存的读写权限(ie. /dev/shm/snap.SNAP_NAME.*)

· 相同应用的不同进程之间互相发送signal的权限
#### 安装模式

snap通过不同的安装模式提供不同的资源访问控制。
1) Devmode

devmode即为开发模式。使用以下命令将应用安装在此模式下：

$ snap install hello --devmode
$ snap list
Name         Version       Rev   Developer  Notes
core          16-2.26.9     2381  canonical  -
hello          2.10          20    canonical  devmode
pc            16.04-0.8     9     canonical  -
pc-kernel     4.4.0-83.106  68    canonical  -

此模式为应用程序提供完全的访问权限，但会在日志中记录程序的越权行为。

在devmode下，snap应用只能访问/snap/下的文件。
2) Classic

此模式将取消所有访问限制，不会在日志中记录越权行为。

在classic模式下，snap应用可以访问’/’下的文件。
#### Interfaces

除去默认安全策略为其提供的资源外，snap应用没有权限访问系统其它资源。若snap应用需要使用系统资源或其它应用程序提供的资源，需通过interfaces机制配置接口。interfaces接口分为两种，slot(服务提供者)和plug(服务使用者)。 
snap应用访问受限资源的示意如下：

![](http://www.ubuntukylin.com/upload/201708/1501752836565131.png)

注意：操作系统在snap系统中也作为snap应用的形式存在。 
如图所示，通过配置snap应用的plug和slot即可实现snap应用的互相访问。 
查看系统上已经存在的plug和slot：

$ snap interfaces
Slot                                              Plug
:account-control                             -
:alsa                                                -
:autopilot-introspection                 -
:bluetooth-control                          -
:browser-support                            -
:camera                                          -
:classic-support                         classic
:core-support                 core:core-support-plug
.........
下面以一个例子说明plug和slot的使用。

name: blue
...
apps:
  blue:
    command: bin/blue
    slots: 【bluez】    

以上文件可作为一个蓝牙设备驱动程序的snap包打包控制文件。当此应用被安装时，系统将为其分配security policy ID为snap.blue.blue并包含规则：当blue启动时为其创建bluez slot。 
要在其它应用中使用这个slot提供的功能，则打包控制文件如下所示：

name: blue-client
...
apps: 
  blue-client:
    command: bin/blue-client
    plugs: 【bluez】

同理，当此应用被安装时，系统将为其分配security policy ID为snap.blue-client.blue-client并包含规则：允许此应用与snap.blue.blue通信。同时，提供slot的安全规则也会改写为：snap.blue.blue允许snap.blue-client.blue-client与其进行通信。 
下图说明了snap应用与应用之间在严格的分隔限制下的互相通信。

![](http://www.ubuntukylin.com/upload/201708/1501752890346136.png)



snap系统由snap应用组成，包括系统和内核都以snap包的形式出现在系统中。各个snap包之间通过interfaces互相提供服务来完成协同工作，同时各个应用又不失自身的独立性。

 
### 总结

snap系统提供了强大的安全系统。与传统linux发行版相比，snap系统中的应用更加独立、安全，同时对snap应用权限的配置也更加简单。在日益增长的嵌入式和物联网需求与日益严峻的系统安全形势下，snap系统表现出了比传统linux发行版更突出的优势。
