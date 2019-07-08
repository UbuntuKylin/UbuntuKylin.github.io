---
title: DigiKam 5.0 发布，快下载到 Ubuntu Kylin 吧！
toc: true
date: 2019-06-24 09:13:05
tags:
categories:
---





## DigiKam 5.0 发布，快下载到 Ubuntu Kylin 吧！

![](http://www.ubuntukylin.com/upload/201607/1468466249346617.jpg)

Linux 中最好用的照片软件之一“DigiKam”，终于在 2016 发布最新版本 5.0。

DigiKam 是一款适应于 Linux、Windows 和 Mac OSX 平台的先进数码照片管理软件。如果你有一台数码单镜反光相机，且想在 Ubuntu Kylin 系统中查看、管理、编辑、分享照片等，digiKam 就是最好的选择。

DigiKam 是一个 KDE 桌面环境的影像管理和编辑程式。它支持所有主要的图像格式，并可以组织目录为基础的照片收藏，或按日期、时间、标签的动态相册。用户还可以对图像添加标题和评语，搜索他们和透过智能文件夹保存搜索。加入插件还可以输出到 Flickr 的相册、Gallery2、谷歌地球的的 KML 文件、Simpleviewer、刻录成光盘或创建Web画廊。

通过本次发布，DigiKam 计划新版发布将会周期更短。所以，对于用户来说再也不用等很多年才能迎来全新的功能。

现在，就让我们来看看 DigiKam 5.0 版的主要特性。

### DigiKam 5.0 特性介绍

有很多的变化都是体现在代码中，所以你可能无法直接看到，但是在使用时，就会有不一样的感觉。

 * 实现多线程查询数据库

 * 通过新的同步工具，增强元数据的工作流

 * 给 Qt 5 增加 kipi 插件接口

 * 更新数据库代码和新的数据库配置面板

 * 可以在第一次运行的时候就设置 MySQL 数据库

### 在 Ubuntu Kylin 16.04 中安装 DigiKam 5.0

由于最新版本在官方软件仓库中还无法下载，所以提供了一个非官方的 PPA。打开终端并一一运行如下命令：
sudo add-apt-repository ppa:philip5/extra
sudo apt update
sudo apt install digikam5
以上PPA只对 Ubuntu Kylin 16.04 和 15.10 有效。

Digikam 是一个约有 400MB 的应用程序。安装后，你可以通过 Dash 查找和搜索 DigiKam 打开并运行。在第一次运行时，会有一些配置选择。

### 在 Ubuntu Kylin 16.04 中卸载 DigiKam 5.0

如果你想卸载通过上面PPA安装的 DigiKam，可使用如下命令：
sudo apt remove digikam5
sudo add-apt-repository --remove ppa:philip5/extra


