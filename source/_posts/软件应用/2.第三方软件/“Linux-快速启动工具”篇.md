---
title: '“Linux 快速启动工具”篇 '
toc: true
date: 2019-06-29 11:46:38
tags:
categories:
---





## “Linux 快速启动工具”篇

本项目最终实现的方案是python+qt+qml。python主要是引用xlib实现热键功能，qt主要写配置界面，qml做的是长按super显示的view。

首先是配置界面，这个先用qt实现，后来又转到pyqt。这是一个很普通的窗体界面，一个QListView，几个QPushButton，点Add之后打开添加界面，输入各种信息。这个界面很简单，各种GUI库都能实现，选择pyqt的话生成配置文件比较方便，因为python有强大的cPickle模块。配置这块的话自定义了一个数据结构，然后用cPickle模块导入导出，文件操作很方便。打开配置界面的时候，load配置文件，添加或者删除的时候dump一下就行。

启动的view这块用qml做的,因为对qml不是很熟悉。现在采用的是程序生成qml文件的方式，而且动态更新现在还有问题，配置完之后得重启。这块的话会在下个版本中修复。

![](https://www.ubuntukylin.com/upload/images/destop.png)

 

   经过修改，通过Xlib的调用实现该功能。

   现在程序的基本流程是：

按super键，super计时器开始计时，super的flag设为true，当计时器达到某一值的时候，显示启动view，放开super，停止计时。

   当super键位true时，检测到其他注册按键，启动相应程序。

   托盘有两个选项：设置和退出。设置选项打开配置界面，退出选项退出程序

   目前还存在的问题：

   1、因为qt托盘的bug，有些系统显示不正常，如ubuntu。

   2、系统文件io过多，有时候有卡顿现象，这个得逐步优化。

   3、UI还有待改善。

   4、还有一些隐藏bug，需要全面测试。

 