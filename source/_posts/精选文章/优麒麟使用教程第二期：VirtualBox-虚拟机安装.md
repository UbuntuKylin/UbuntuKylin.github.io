---
title: 优麒麟使用教程第二期：VirtualBox 虚拟机安装
toc: true
date: 2019-06-24 08:58:41
tags:
categories:
---





## 优麒麟使用教程第二期：VirtualBox 虚拟机安装

在上一期使用教程中，小编已经介绍了如何在 VMWare 中安装和使用优麒麟，接下来，小编继续展示在 VirtualBox 中如何操作。同时我们下一期会继续推出“优麒麟使用教程第三期：Windows 平台 U 盘启动盘制作”，敬请期待！

一.下载系统镜像

1、下载优麒麟镜像。进入优麒麟官网 [点击此处](www.ubuntukylin.com/downloads) 下载最新版 19.04 并检查 MD5 值。

![](http://www.ubuntukylin.com/upload/201906/1559807385841105.jpg)

二. 在 VirtualBox 中创建和配置虚拟机

1、设置虚拟机的名称和系统类型。单击“新建”按钮，新建一个虚拟机。在“名称”中输入虚拟机的名称，如：优麒麟 19.04。类型选择“ Linux ”，版本选择“ Ubuntu(64_bit) ”。单击“下一步”。

![](http://www.ubuntukylin.com/upload/201906/1559807493968673.jpg)

2、设置虚拟机的内存大小。建议大小为 2048M 以上，这里将虚拟内存设为 4G ，然后单击“下一步”。

![](http://www.ubuntukylin.com/upload/201906/1559807510902821.jpg)

3、创建虚拟硬盘。选择“现在创建虚拟硬盘”，单击“创建”。

![](http://www.ubuntukylin.com/upload/201906/1559807409766788.jpg)

4、设置虚拟硬盘的文件类型。选择默认的 VDI（ VirtualBox 磁盘映像），单击“下一步”。

![](http://www.ubuntukylin.com/upload/201906/1559807523862960.jpg)

5、设置存储在物理硬盘上的的方式。选择“动态分配”，这样可以在使用时占用磁盘空间，关闭时释放空间，单击“下一步”。

![](http://www.ubuntukylin.com/upload/201906/1559807533905938.jpg)

6、设置虚拟硬盘的文件位置和大小。虚拟硬盘大小应至少为 12G，此处我们设置为 55G，单击“创建”。

![](http://www.ubuntukylin.com/upload/201906/1559807542619752.jpg)

7、虚拟机创建完成。在界面中可以看到之前创建虚拟机的名称、内存大小、硬盘大小等信息。一台类似实体机的电脑已准备完毕，接下来我们可以开始安装系统了。

![](http://www.ubuntukylin.com/upload/201906/1559807553949170.jpg)

三、在虚拟机中安装优麒麟系统

1、启动虚拟机。双击启动或右击选择“启动”。
![](http://www.ubuntukylin.com/upload/201906/1559807553949170.jpg)

2、为启动盘加载镜像。在弹出的对话框中，单击文件夹图标，选择优麒麟镜像，然后单击“启动”。

![](http://www.ubuntukylin.com/upload/201906/1559807807334725.png)

3、 设置系统语言。根据使用需求选择语言，默认选项为“中文（简体）”，然后单击“安装 Ubuntu Kylin ”（也可点击“试用 Ubuntu Kylin ”，进行试用体验后再进行安装）。

![](http://www.ubuntukylin.com/upload/201906/1559807690342917.png)

4、设置键盘布局。选择“汉语”，单击“继续”。

![](http://www.ubuntukylin.com/upload/201906/1559807824917246.png)

5、设置安装时更新和其他软件方式。 如果已联网，可选择“安装 Ubuntu Kylin 时下载更新”。

![](http://www.ubuntukylin.com/upload/201906/1559807834830589.png)

6、设置系统安装类型。虚拟机中可直接选择“清除整个磁盘并安装 Ubuntu Kylin ”，执行全盘安装，单击“现在安装”继续。此处会弹出磁盘格式化警告框，选择“继续”即可。

![](http://www.ubuntukylin.com/upload/201906/1559807852555967.png)

7、设置系统时区。单击地图中的“中国”区域，即显示“ Shanghai ”，单击“继续”。

![](http://www.ubuntukylin.com/upload/201906/1559807879121568.png)

8、设置系统登录用户名和密码。用户名要求以小写字母开头，单击“继续”。

![](http://www.ubuntukylin.com/upload/201906/1559807892741221.png)

9、接下来就是约二十分钟的系统安装时间，请耐心等待。

![](http://www.ubuntukylin.com/upload/201906/1559807904337145.png)

10、提示系统安装完毕后，点击“现在重启”，然后在关机动画界面根据提示，按“ Enter ”键退出安装介质。成功重启后进入优麒麟系统。

![](http://www.ubuntukylin.com/upload/201906/1559807946247082.jpg)
