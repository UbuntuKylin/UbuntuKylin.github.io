---
title: 快速检查电脑是否配备USB 3.0
toc: true
date: 2019-06-29 11:53:54
tags:
categories:
---

 
越来越多的电脑开始配备USB 3.0端口，但是如何知道您的电脑是否带有3.0端口以及哪个端口是3.0呢？方法如下：
打开终端，使用以下命令： 
$ lsusb 
该命令显示系统中的USB相关信息，检查结果，如果发现乐死“3.0 root hub”字样，表明系统带有USB 3.0。
<img src="http://www.ubuntukylin.com/upload/images/usb30.png"></img> 
接下来，如何识别哪个端口为USB 3.0呢？ 
通常USB 3.0端口带有SS标记（Super Speed的缩写）。如果硬件厂商没有标记SS或USB 3，则检查端口内部的颜色，USB 3.0通常为蓝色。
<img src="http://www.ubuntukylin.com/upload/images/usb3_0port.jpg"></img>
