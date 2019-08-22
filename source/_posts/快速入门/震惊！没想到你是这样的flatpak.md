---
title: 震惊！没想到你是这样的flatpak...
toc: true
date: 2019-06-24 09:04:06
tags:
categories:
---





## 震惊！没想到你是这样的flatpak...

![](http://www.ubuntukylin.com/upload/201707/1500013249421469.jpg)

**引言**

之前我们介绍过如何在优麒麟和银河麒麟社区版上构建snap/flatpak包（传送门）,今天我们来更深入的认识下flatpak：

 

**Flatpak**(前世为xdg-app) 是一种用于构建，分发，安装和运行应用程序的技术。它主要针对的是Linux桌面，通过在沙箱中隔离应用程序来提高Linux桌面的安全性，允许应用程序安装在任何Linux发行版上。

 

### 历史：

2013: 在[GNOME Developer Experience hackfest, Brussels](https://wiki.gnome.org/DeveloperExperience/Hackfest2013)大会后，萌生在GNOME中使用应用程序容器技术的念头，次年开始开发。

2016年5月: 第一个主版本xdg-app发布。

　　 　6月：重命名为flatpak。

　　　 8月：endless OS 3.0, 第一个默认支持Flatpak的发行版。
　　　
　　　 11月：ClearLinux声明采用flatpak。

2017年2月： 最新的flatpak已经可以在Arch, Debian, Fedora, Gentoo, Mageia, openSUSE, Ubuntu等的最新版本上运行。

 

### 基本概念：

#### 运行时(runtimes)

“运行时”提供应用程序所需的基本依赖。有各种各样的“运行时”,比如“Freedesktop运行时”，“GNOME运行时”。“Freedesktop运行时”包含一系列必要的库和服务，包括D-Bus, GLib, PulseAudio, X11和Wayland等。“GNOME运行时”基于“FreeDesktop运行时”，增加了一些GNOME平台相关的库，比如GStreamer, GTK+, GVFS等。必须针对运行时构建每个应用程序，并且必须在主机系统上安装此运行时才能运行应用程序。用户可以同时安装多个不同的运行时，包括不同版本的同一个运行时。KDE runtime正在开发中。

每一个运行时可以看做一个’/usr’ 文件系统，当程序运行时，它的运行时挂载在‘/usr’上。

 

#### 捆绑库(Bundled libraries)

当一个程序需要的依赖不在运行时中，使用捆绑库来绑定这些依赖到程序上。

 

#### SDK（软件开发套件）

SDK也是一个“运行时”，是用于构建应用程序的特殊类型的运行时，它包含了构建和打包工具（‘devel’ parts），如头文件，编译器和调试器。通常，SDK与“运行时”配对，由应用程序使用。

 

#### 扩展（Extensions）

一个扩展是对于运行时或程序的可选插件，一般用于把translations和debug信息从运行时分离出来，比如, org.freedesktop.Platform.Locale 可以追加到org.freedesktop.Platform运行时上用来添加翻译。

 

#### 沙箱（Sandbox）

使用Flatpak，每个应用程序都是在孤立的环境中构建和运行的。默认情况下，应用程序只能“查看”自身及其“运行时”,访问用户文件，网络，graphics sockets，总线和设备上的子系统必须明确授予权限，访问其他内容（如其他进程）是不允许的。（可以通过Portals机制在沙箱内访问外面系统，比如打印，截图等）

 

### 原理：

Flatpak主要使用了如下技术：

1. [bubblewrap](https://github.com/projectatomic/bubblewrap)：依赖它作为沙箱的底层实现, 限制了应用程序访问操作系统或用户数据的能力，并且提供了非特权用户使用容器的能力。

2. Systemd：将各个subsystem和cgroup树关联并挂载好，为沙箱创建 cgroups。

3. D-Bus, 为应用程序提供高层APIs。

4. 使用Open Container Initiative的OCI格式作为单文件的传输格式，方便传输。

5. 使用OSTree系统用于版本化和分发文件系统树。

6. 使用Appstream 元数据，使得Flatpak应用程序在软件中心可以完美呈现出来。

而其中最重要的当属bubblewrap，它是整个应用沙箱构建的关键，主要利用了如下内核特性： 

#### Namespaces:

命名空间是对全局系统资源的一个封装隔离，使得处于不同namespace的进程拥有独立的全局系统资源，改变一个namespace中的系统资源只会影响当前namespace里的进程，对其他namespace中的进程没有影响。它控制了进程的可见范围，例如网络、挂载点、进程等等。同时使得非特权用户可以创建沙箱。它有以下几类：

● Mount namespace (CLONE_NEWNS): 

用来隔离文件系统的挂载点, 使得不同的mount namespace拥有自己独立的挂载点信息，不同的namespace之间不会相互影响，这对于构建用户或者容器自己的文件系统目录非常有用。bubblewrap 总是创建一个新的mount namespace, root挂载在tmpfs上，用户可以明确指定文件系统的哪个部分在沙盒中是可见的。

● User namespaces (CLONE_NEWUSER): 

用来隔离用户权限相关的Linux资源，包括用户ID 和组ID， 在不同的user namespace中，同样一个用户的user ID 和group ID可以不一样，换句话说，一个用户可以在父user namespace中是普通用户，在子user namespace中是超级用户（超级用户只相对于子user namespace所拥有的资源，无法访问其他user namespace中需要超级用户才能访问资源）。

● IPC namespaces (CLONE_NEWIPC): 

沙箱会得到所有不同形式的IPCs的一份拷贝，比如SysV 共享内存和信号量等。

● PID namespaces (CLONE_NEWPID): 

用来隔离进程的ID空间，沙箱内的程序看不见任何沙箱外的进程，此外, bubblewrap 会运行一个pid为1的程序在容器中,用来处理回收子进程的需求。

● Network namespaces (CLONE_NEWNET): 

用来隔绝网络，在它自己的network namespace中只有一个回环设备。 

● UTS namespace (CLONE_NEWUTS):

允许沙箱拥有自己独立的hostname和domain name.

#### Cgroups:

cgroup和namespace类似，也是将进程进行分组，但它的目的和namespace不一样，namespace是为了隔离进程组之间的资源，而cgroup是为了对一组进程进行统一的资源监控和限制。

#### Bind Mount:

将一个目录（或文件）中的内容挂载到另一个目录（或文件）上.

#### Seccomp rules：

Linux kernel 所支持的一种简洁的sandboxing机制。它能使一个进程进入到一种“安全”运行模式，该模式下的进程只能调用4种系统调用（system calls），即read(), write(), exit()和sigreturn()，否则进程便会被终止。

同时，bubblewrap 使用PR_SET_NO_NEW_PRIVS 关闭 setuid 二进制程序。

当一个进程或其子进程设置了PR_SET_NO_NEW_PRIVS 属性,则其不能访问一些无法share的操作,如setuid, 和chroot。

 

### 实验：

接下来，我们通过如下方式进入到一个flatpak创建的沙箱中：

安装程序所需的“运行时”和Sdk：

$ flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo

$ flatpak install gnome org.gnome.Platform//3.24 org.gnome.Sdk//3.24

安装gedit:

$ flatpak remote-add --from gnome-apps https://sdk.gnome.org/gnome-apps.flatpakrepo

$ flatpak install gnome-apps org.gnome.gedit

创建一个‘devel sandbox’中的shell:

$ flatpak run --devel --command=bash org.gnome.gedit

可以看到此沙箱中有３个进程，且flatpak-bwrap pid为1。

$ ps

  PID TTY          TIME CMD

   1 ?        00:00:00 flatpak-bwrap

   2 ?        00:00:00 bash

   5 ?        00:00:00 ps

查看当前进程所属的namespace，括号里的数字标识不同的namespace：

$ ls -l /proc/&&/ns

total 0

 15:48 cgroup -> cgroup:【4026531835】

 15:48 ipc -> ipc:【4026531839】

 15:48 mnt -> mnt:【4026532241】

 15:48 net -> net:【4026532244】

 15:48 pid -> pid:【4026532242】

 15:48 user -> user:【4026532371】

 15:48 uts -> uts:【4026531838】

然后在主机中打开另一个终端，查看主机中当前进程的namespace:

$ ls /proc/&&/ns

total 0

 15:56 cgroup -> cgroup:【4026531835】

 15:56 ipc -> ipc:【4026531839】

 15:56 mnt -> mnt:【4026531840】

 15:56 net -> net:【4026531957】
 
 15:56 pid -> pid:【4026531836】

 15:56 user -> user:【4026531837】

 15:56 uts -> uts:【4026531838】

可以看到沙箱中的进程所属的namespace与主机环境下进程的namespace相比，它们的mount ,net, pid, user namespace不同，这时我们在主机环境下把ping文件拷贝进主目录（gedit声明了对’/home’的访问权限），然后在sandbox shell中执行ping 192.168.0.1，会发现报错：

$ ./ping 192.168.0.1

ping: socket: Operation not permitted

因为gedit没有申请网络权限，它和主机在不同的network namespaces中。

 

怎么样，是不是很有趣，你还能在这个沙箱中做更多有趣的探索，行动起来，一起来flatpak吧！
