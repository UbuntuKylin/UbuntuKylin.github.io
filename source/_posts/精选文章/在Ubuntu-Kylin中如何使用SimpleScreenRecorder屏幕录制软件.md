---
title: 在Ubuntu Kylin中如何使用SimpleScreenRecorder屏幕录制软件
toc: true
date: 2019-06-24 14:25:09
tags:
categories:
---





## 在Ubuntu Kylin中如何使用SimpleScreenRecorder屏幕录制软件

英文原文：[点击此处](http://itsfoss.com/record-screen-ubuntu-simplescreenrecorder/) 翻译：Limy

你曾见过一些在Linux系统上录制很炫的视频吗？你曾思考过那些人在Ubuntu Kylin或者其他一些Linux系统上如何录制的呢？也许都曾尝试这样想过，但却无法找到一些软件来录制屏幕。今天，让我来告诉你如何在Ubuntu Kylin操作系统上录制屏幕。

我们将使用SimpleScreenRecorder屏幕录制软件来解决这个问题。首先来看看，如何在Ubuntu Kylin 14.04、Ubuntu Kylin 14.10安装SimpleScreenRecorder。

 

### 安装SimpleScreenRecorder

如果simplescreenrecorder已包含在软件源，可直接通过软件中心或在终端运行下面的命令来安装：

sudo apt-get install simplescreenrecorder

![](http://www.ubuntukylin.com/upload/images/r2.png)

如果不在软件源中，则可以使用官方的PPA。在终端运行以下命令：

sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder
    sudo apt-get update
    sudo apt-get install simplescreenrecorder

 

### 设置SimpleScreenRecorder

一旦安装完SimpleScreenRecorder，您可能希望根据自己的需求来配置。

1.通过Dash或Gnome打开软件中心，搜索并打开SimpleScreenRecorder。

![](http://www.ubuntukylin.com/upload/images/r3.png)

![](http://www.ubuntukylin.com/upload/images/r4.png)

2.选项设置。例如可设置录制视频的屏幕大小。如果你想录制固定的区域或跟随鼠标等，也可在对话框中选择。并且可设置是否要录制光标和声音。就个人而言，我的电脑是PC音频插孔耳机，所以我选择“Monitor of 内部音频，模拟立体声”。

![](http://www.ubuntukylin.com/upload/images/r5.png)

3.点击“继续”。在下一个对话框中，选择要保存视频文件的位置，并将视频的音频保存为比特率。

![](http://www.ubuntukylin.com/upload/images/r6.png)

4.以上几步设置好后，进入到下一步开始录制。点击"开始录制"按钮，它将开始为你录制屏幕。

![](http://www.ubuntukylin.com/upload/images/r7.png)

如果你想让它停止录制，只需回到SimpleScreenRecoder应用程序点击“停止录制”按钮。然后您的视频将默认被保存在指定的位置。

当然在Ubuntu、Ubuntu Kylin 或其他Linux系统上会有其他更多、更好的视频录制软件。然而，目前在使用中，我觉得SimpleScreenRecorder是最好用的，因为它能够找到与我的电脑对应的音频插孔同步起来。并且，它使用简单，录制的画面也很清晰！