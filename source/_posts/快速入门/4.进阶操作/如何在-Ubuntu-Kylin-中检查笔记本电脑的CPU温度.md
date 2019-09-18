---
title: 如何在 Ubuntu Kylin 中检查笔记本电脑的CPU温度
toc: true
date: 2019-06-24 14:28:35
tags:
categories:
---


![](http://www.ubuntukylin.com/upload/images/tempreture0.png)

笔记本电脑过热是这些天大家面临的一个共同问题，监测硬件温度可以帮助您诊断为什么笔记本电脑会越来越烫，在这篇文章中，我们将看到如何在 Ubuntu Kylin 中检查CPU温度。

我们将使用GUI工具Psensor帮助您监视硬件温度。Psecsor具有以下功能：

 * 监控主板和CPU传感器的温度
 * 监测NVIDIA GPU的温度
 * 监控硬盘驱动器的温度
 * 监测风扇的旋转速度
 * 监视CPU的使用率

最新版Psensor还提供了Indicator小程序，您可以将硬件温度监控在顶部面板上，当温度超过限值时发送一个桌面通知。

**如何在 Ubuntu Kylin 15.04 和 14.04 版本中安装 Psensor**

在安装Psensor之前，您需要安装和配置lm-sensors，这是一个用于硬件监控的命令行实用程序。如果你还想测量硬盘温度，请安装hddtemp。请在终端中运行如下命令：
　　sudo apt-get install lm-sensors hddtemp

为了确保它的工作原理，运行下面的命令
　　sudo sensors-detect

如果安装正确，终端会输出类似以下内容：
　　acpitz-virtual-0

　　Adapter: Virtual device

　　temp1: +43.0°C (crit = +98.0°C)

　　coretemp-isa-0000　

　　Adapter: ISA adapter

　　Physical id 0: +44.0°C (high = +100.0°C, crit = +100.0°C)

　　Core 0: +41.0°C (high = +100.0°C, crit = +100.0°C)

　　Core 1: +40.0°C (high = +100.0°C, crit = +100.0°C)

然后您可以使用以下命令安装Psensor：
　　sudo apt-get install psensor

安装完成后，可以通过Dash找到并运行Psensor应用程序。第一次运行时需按提示进行简单配置。

![](http://www.ubuntukylin.com/upload/images/tempreture1.png)

您还可以设置在应用指示器菜单中显示温度：

![](http://www.ubuntukylin.com/upload/images/tempreture2.png)

赶紧试一下，用Psensor帮您找出哪个进程让计算机过热吧。
