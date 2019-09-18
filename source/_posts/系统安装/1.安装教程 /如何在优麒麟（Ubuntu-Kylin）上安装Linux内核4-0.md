---
title: '如何在优麒麟（Ubuntu Kylin）上安装Linux内核4.0 '
toc: true
date: 2019-06-24 14:29:49
tags:
categories:
---


4月12日是所有的开源运动爱好者的大日子，Linus Torvalds 宣布了 Linux 内核4.0的发布。其代号为‘Hurr durr I'm a sheep’，是目前为止最新的主干内核。而上一个稳定内核为3.19.4。4.0是一个比较重要的版本，包括了一些很棒的功能，例如无重启补丁(实时补丁)、新的升级驱动、最新的硬件支持以及很多有趣的功能，但Linus表示4.1会是一个更重要的版本。

警告：安装新的内核可能会导致你的系统不可用或不稳定。如果你仍然使用以下命令继续安装，请确保备份所有重要数据到外部硬盘。
**在 Ubuntu Kylin 15.04 上安装Linux内核4.0**

如果你正在使用 Ubuntu Kylin 15.04，可以直接通过Ubuntu内核网站安装最新的Linux内核4.0。请在终端中运行以下命令。
**在64位 Ubuntu Kylin 15.04**

1. $ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.0-vivid/linux-image-4.0.0-040000-generic_4.0.0-040000.201504121935_amd64.deb 

2. $ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.0-vivid/linux-headers-4.0.0-040000-generic_4.0.0-040000.201504121935_amd64.deb 

3. $ sudo dpkg -i linux-headers-4.0.0*.deb linux-image-4.0.0*.deb
**在32位 Ubuntu Kylin 15.04**

1. $ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.0-vivid/linux-image-4.0.0-040000-generic_4.0.0-040000.201504121935_i386.deb 

2. $ wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.0-vivid/linux-headers-4.0.0-040000-generic_4.0.0-040000.201504121935_i386.deb 

3. $ sudo dpkg -i linux-headers-4.0.0*.deb linux-image-4.0.0*.deb

 
