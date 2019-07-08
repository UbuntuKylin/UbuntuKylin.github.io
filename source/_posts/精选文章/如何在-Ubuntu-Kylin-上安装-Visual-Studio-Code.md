---
title: 如何在 Ubuntu Kylin 上安装 Visual Studio Code
toc: true
date: 2019-06-24 14:30:00
tags:
categories:
---





## 如何在 Ubuntu Kylin 上安装 Visual Studio Code

出乎意料，微软已经发布包括 Linux 在内的所有主流桌面平台的 Visual Studio Code。作为 Ubuntu Kylin 用户，您可以通过 Ubuntu Make 工具轻松完成 Visual Studio Code 的安装，快速开始Web开发。

Ubuntu Make 的前身为 Ubuntu 开发者工具中心，是一个命令行实用程序，可让您轻松地安装各种开发工具、语言和IDE。通过 Ubuntu Make ，您可以轻松地安装 Android Studio 和 Eclipse 等流行的 IDE。在本教程中我们将看到如何在 Ubuntu Kylin 上安装 Visual Studio Code 与 Ubuntu Make。

在 Ubuntu Kylin 中安装 Microsoft Visual Studio Code

在安装 Visual Studio Code 之前，我们需要先安装 Ubuntu Make。虽然 Ubuntu Make 已在 Ubuntu Kylin 15.04 的软件仓库中，但是您需要的是 Ubuntu Make 0.7 for Visual Studio。您可以通过官方的PPA下载最新的 Ubuntu Make。该PPA对 Ubuntu Kylin 14.04，14.10和15.04可用，仅可用于64位平台。

打开终端，使用下面的命令来通过官方PPA来安装 Ubuntu Make：

 * sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make

 * sudo apt-get update

 * sudo apt-get install ubuntu-make

一旦您已经安装上了 Ubuntu Make，可以使用下面的命令来安装 Visual Studio Code：

 * umake web visual-studio-code

您将被要求提供安装路径：

![](http://www.ubuntukylin.com/upload/images/stu1.png)

在一大堆的条款和条件后，程序会询问您是否允许安装 Visual Studio Code。在以下屏幕按“a”键：

![](http://www.ubuntukylin.com/upload/images/st2.png)

接受条款之后，程序会自动开始下载并安装 Visual Studio Code。安装完成后，Visual Studio Code 的图标将锁定到启动栏，点击即可运行。下图是V isual Studio Code 的运行截图，整体视觉风格与 Ubuntu Kylin 15.04 完全统一：

![](http://www.ubuntukylin.com/upload/images/st2.png)

在 Ubuntu Kylin 上卸载 Visual Studio Code

要卸载 Visual Studio Code，我们将使用相同的命令行工具umake。

在终端使用下面的命令：

 * umake web visual-studio-code --remove

如果您不想使用 Ubuntu Make，也可以通过微软官网下载的 Visual Studio Code 安装文件直接安装：[点击此处](https://code.visualstudio.com/Download)

您看，在 Ubuntu Kylin 中安装 Visual Studio Code 是多么容易，赶紧动手试试吧，希望本教程能够帮助到您。

 
