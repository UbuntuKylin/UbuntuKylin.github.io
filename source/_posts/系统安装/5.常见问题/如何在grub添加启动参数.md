---
title: 如何在grub添加启动参数
toc: true
date: 2020-08-28 19:26:55
tags:
categories:
---





## 如何在grub添加启动参数
对于grub2，ubuntu给了一个官方的配置文件/etc/default/grub。大部分情况下grub2的设置都可以在这个文件中搞定，而且这个文件结构也比较简单，修改起来也容易。完全没有必要直接改/boot/grub/grub.cfg或者/etc/grub.d/下的文件。

修改/etc/default/grub只需简单一个命令：sudo vim /etc/default/grub
下面是系统默认的内容，以及最常用的修改菜单显示时间和默认操作系统的方法：
 #If you change this file, run 'update-grub' afterwards to update
 #/boot/grub/grub.cfg.

GRUB_DEFAULT=0 #将0改为saved，可让grub记住上次启动时选择的系统
GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
GRUB_TIMEOUT="5" #显示启动选择菜单的时间
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""

修改完成后执行以下命令：

$ sudo apt-get install grub2-common  //没有 update-grub命令时,先运行这个安装命令

$ sudo update-grub  //生成grub的配置文件

即可。
