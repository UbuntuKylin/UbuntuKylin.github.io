---
title: Ubuntu Kylin 14.04 版本默认启动HDMI无声音问题的修复
toc: true
date: 2019-06-29 11:51:59
tags:
categories:
---


Ubuntu Kylin 中的声音问题是一个老生常谈的问题。

在这里我们所使用的环境为Ubuntu Kylin 14.04版，安装完之后第一次启动系统没有声音。经过排查发现alsamixer状态怪异:

<img src="http://www.ubuntukylin.com/upload/images/%E5%9B%BE%E7%89%8722.jpg"></img>

如图所示：alsamixer中默认情况下设置的是HDMI。这意味着默认情况下，声音输出为HDMI，而不是内置扬声器。所以在系统中我们找不到内置扬声器设置。

打开终端，使用以下命令检查alsamixer状态：

alsamixer

如果alsamixer中默认情况下为HDMI或其他音频输出设置，请继续阅读下文看如何可以修复它。

现在我们要做的是强制Ubuntu Kylin默认使用模拟输出而不是HDMI接口，在这里我们需要一些信息。打开终端，然后输入下面的命令：

aplay -l

终端将列出设备，卡号等信息。记下卡号和模拟输出设备号。我的输出结果是这样的：

<img src="http://www.ubuntukylin.com/upload/images/%E5%9B%BE%E7%89%8723.jpg"></img>

一旦你有需要的卡和设备编号，就可以做出这样一个新的配置文件：

sudo gedit /etc/asound.conf

上面的命令也将打开该文件。当然，用你的卡和设备号替换添加以下几行：

defaults.pcm.card 1

defaults.pcm.device 0

保存文件并重新启动计算机。你现在应该可以听到声音了。值得注意的是，这个问题的修复适用于所有的Linux发行版，如Linux Mint的，Elementary OS，Fedora，Arch Linux等。当然，这种“无声音修复”仅适用于当HDMI是默认设置的情况下。
