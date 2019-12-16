---
title: '在双系统（Windows 8 、Ubuntu Kylin）中如何从Windows 8卸载Ubuntu Kylin '
toc: true
date: 2019-06-29 11:47:58
tags:
categories:
---


![](https://www.ubuntukylin.com/upload/images/q1.jpg) 

曾几次介绍如何在Windows 8存在的情况下安装Ubuntu Kylin。但是，我们如何从Windows 8中卸载Ubuntu Kylin呢？这篇教程适用于任何Linux操作系统，如Ubuntu Kylin、Linux Mint、Elementary或任何其他Linux的发行版。

如果您认为卸载Ubuntu Kylin是一个艰巨的任务，那完全是错误的，因为从Windows中删除Ubuntu Kylin是很容易的。如果你有一个Windows安装盘，从Windows中卸载Linux简直就是小菜一碟。

本教程教你当启动了Windows 8/8.1安装盘时如何从Windows 8或Windows 8.1中彻底删除Linux。

从双系统中安全卸载Ubuntu Kylin

如果您有Windows 8安装盘并且已经安装了Windows 8.1操作系统，它的运行过程都是一样的,虽不与Windows 7相同。如果有Windows安装盘，就来一起学习下面这个在Windows中删除Ubuntu Kylin Linux操作系统的过程。

从双系统中删除Linux分两部分进行。首先是删除已安装Linux的分区（S）。由于只删除Linux分区会导致Grub错误，所以第二部分是修复Windows启动加载器。

第一部分：在Windows中删除Linux分区

第1步：登录Windows。按Windows+ R，运行diskmgmt.msc命令打开Windows的磁盘管理工具。

![](https://www.ubuntukylin.com/upload/images/q2.jpg) 

 第2步：既然已经安装了Linux，就很容易让您通过它的容量大小识别Linux分区。另一个提示可以通过看分区是否无文件系统和驱动器号来识别Linux分区。 Windows分区都标有一个驱动器号，如通常在NTFS或FAT文件系统C，D，E等。

正如您所看到的，这有三个Linux分区。

![](https://www.ubuntukylin.com/upload/images/q3.jpg) 

第3步：选择Linux分区（S），右击选择“删除卷”选项。

![](https://www.ubuntukylin.com/upload/images/q4.jpg) 

它会弹出一个警告，在这里选择“是”。

![](https://www.ubuntukylin.com/upload/images/q5.jpg) 

第4步：被删除的分区将作为一大块空闲空间。您可以扩展现有分区或创建一个新的Windows分区出来。如果想双启动Linux与Windows，建议创建一个新的驱动器（或卷或分区，随便您怎么称呼它）。

![](https://www.ubuntukylin.com/upload/images/q6.jpg) 

第二部分：修复Windows启动加载器

一旦删除Linux分区，就需要花时间来修复Windows启动加载器。这里的图片可能有点不清晰，因为Ubuntu Kylin登录界面的截屏比Windows简单。

第1步：放入Windows 8安装盘，重启计算机。在开机时按F10或F12键，进入BIOS/ UEFI，从硬盘启动。

![](https://www.ubuntukylin.com/upload/images/q7.jpg) 

第2步：选择“修复计算机”。

![](https://www.ubuntukylin.com/upload/images/q8.jpg) 

第3步：进入“故障处理”选项。

![](https://www.ubuntukylin.com/upload/images/q9.jpg) 

第4步：在“故障处理”页面中，选择“高级选项”。

![](https://www.ubuntukylin.com/upload/images/q10.jpg) 

第5步：找到”命令提示符”。

![](https://www.ubuntukylin.com/upload/images/q11.jpg) 

第6步：在命令行中输入以下命令来修复Windows启动加载器。

 bootrec.exe /fixmbr

通常情况下，它运行的时间很短。您甚至不必等它。

![](https://www.ubuntukylin.com/upload/images/q11.jpg) 

第7步：一旦完成，重启计算机，这时候从硬盘正常启动，进入Windows。如果您仍看到Grub错误，请尝试以下步骤。

第8步：如果第6步失效，尝试在”高级故障排除”选项中的”自动修复”选项。

![](https://www.ubuntukylin.com/upload/images/q13.jpg) 

这将需要一点时间来找问题，然后修复它。

![](https://www.ubuntukylin.com/upload/images/q14.jpg) 

现在，如果您重启，应该在Windows中正常，就不会看到任何的grub救援错误。

希望这篇技巧文章能帮您从Windows8双系统启动中完全删除Ubuntu Kylin Linux系统。欢迎给UK团队提出任何问题或建议。

 

 
