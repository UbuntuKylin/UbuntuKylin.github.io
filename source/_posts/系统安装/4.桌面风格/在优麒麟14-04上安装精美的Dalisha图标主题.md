---
title: 在优麒麟14.04上安装精美的Dalisha图标主题
toc: true
date: 2019-06-29 11:48:43
tags:
categories:
---

  Dalisha是一套优美的圆角图标，可应用于几乎所有主流的Linux桌面环境，例如Unity、GNOME、KDE、Cinnamon、Mate等。Dalisha拥有超过30,000个图标，目前正处于活跃开发状态。如果您愿意尝试，不妨跟随以下步骤在优麒麟上安装体验。

![](https://www.ubuntukylin.com/upload/images/dalisha-7.jpg) 

**通过PPA在优麒麟上安装Dalisha**
  打开终端，执行以下命令（需要大约120MB的磁盘空间）：

 * sudo add-apt-repository ppa:noobslab/icons

 * sudo apt-get update

 * sudo apt-get install dalisha-icons

     或者通过以下链接地址下载：[点击此处](http://gnome-look.org/content/show.php/Dalisha?content=166286)

**通过优客助手设置试用Dalisha图标主题**
  安装完成之后，打开优客助手，在系统美化标签中选择Dalisha图标主题：

![](https://www.ubuntukylin.com/upload/images/dalisha-2.png) 
  接下来就可以欣赏使用最新的主题风格啦。

![](https://www.ubuntukylin.com/upload/images/dalisha.png) 
卸载Dalisha
  打开命令行，执行以下命令：

 * sudo apt-get remove dalisha-icons 

 * sudo add-apt-repository --remove ppa:noobslab/icons

