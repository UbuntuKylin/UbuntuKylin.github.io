---
title: 在 Ubuntu Kylin 上安装图像处理软件 RawTherapee
toc: true
date: 2019-06-24 14:26:29
tags:
categories:
---


![](https://www.ubuntukylin.com/upload/201603/1457316823398754.png)

如果你是一名业余摄影爱好者或专业摄影师，你可以使用 Adobe Lightroom 编辑处理数码单反相机RAW图像文件，也可以看看其它运行在 Linux 下的替代软件。事实上，在 Linux 中可以用开源软件 Darktable 或 RawTherapee 来替代 Adobe Lightroom。

之前我们已经看过如何在 Ubuntu Kylin 上安装 Darktable，今天我们将看到如何在 Ubuntu Kylin 上安装 RawTherapee。在此之前，让我们快速浏览一下 RawTherapee 的主要功能特点。

### RawTherapee 功能特点：

 * 提供了数字图像的编修功能，支持 RAW、TIFF、PNG 与 JPEG 格式的图像
 * 曝光调整
 * 高光还原
 * 阴影/高光
 * 亮度、对比度、饱和度
 * 锐化
 * 白平衡
 * 通道混合
 * 裁切、调整大小、旋转、失真、色散矫正
 * 批处理
 * 调用其他图片编辑器

### 在 Ubuntu Kylin 上安装 RawTherapee

**安装 RawTherapee：**

sudo add-apt-repository ppa:dhor/myway

sudo apt-get update

sudo apt-get install rawtherapee

**卸载 RawTherappe：**

sudo apt-get remove rawtherapee

sudo add-apt-repository --remove ppa:dhor/myway

对于其他平台，你可以下载可执行文件：下载 [RawTherapee](http://rawtherapee.com/downloads)。
