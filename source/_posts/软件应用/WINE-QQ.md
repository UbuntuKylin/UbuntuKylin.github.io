---
title: WINE QQ
toc: true
date: 2019-06-18 10:04:42
tags:
categories:
---





## 银河麒麟版本安装攻略：
记录于20170503：本条专用于最近出的银河麒麟版本安装QQ，优麒麟版本还是按之前的攻略安装
1、从优麒麟官网（http://www.ubuntukylin.com/application/show.php?lang=cn&id=279）下载QQ压缩包，并减压缩。
2、sudo vim /etc/apt/sources.list 修改源地址为 deb http://archive.kylinos.cn/yhkylin/ juniper main restricted universe multiverse 这其实就是系统默认源地址之一，其余的源地址全部删除，然后运行sudo apt-get update 即可。
3、先运行 sudo dpkg --add-architecture i386 然后直接用 sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb ttf-wqy-microhei_0.2.0-beta-2_all.deb wine-qqintl_0.1.3-2_i386.deb 安装qq的三个包，这时会报依赖问题，用 sudo apt-get  -f install 解决依赖即可安装成功，其它使用问题见帖子下文要注意事项。

注意：银河麒麟版不需要像优麒麟版那样去下载帖子末尾的包，源中已有。

===============================================================================

优麒麟版本安装攻略：
记录于20170106：现在这个版本qq登录时会报 “您的号码暂时不能使用低版本的QQ,请到:***下载安装最新版的QQ” ，这是由于被安全机制检测到版本太低，需要手机登录qq将手机设备锁关掉才行。

另外：ubuntu1610之后系统版本的用户，由于ubuntu源里面不再有libpng12这个包了，会包依赖错误，需要手动下载安装libpng12这个包，依赖包已经上传，在文章末尾处可点击下载。 下载后先运行 sudo dpkg --add-architecture i386 后再 sudo dpkg -i libpng12-0_1.2.54-1ubuntu1_i386.deb 即可安装。

=========================================================

由于Wine QQ一直没更新版本导致目前版本报版本过低无法使用，暂时先上UK官网的国际版Wine QQ，虽然功能没那么新，但稳定能用：
发
下载：
下载地址：http://www.ubuntukylin.com/application/show.php?lang=cn&id=279

下载后解压得到wine-qqintl文件夹，里面有三个deb包：fonts-wqy-microhei_0.2.0-beta-2_all.deb、ttf-wqy-microhei_0.2.0-beta-2_all.deb、wine-qqintl_0.1.3-2_i386.deb

安装：
1、在wine-qqintl目录下打开终端输入：sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb ttf-wqy-microhei_0.2.0-beta-2_all.deb wine-qqintl_0.1.3-2_i386.deb
2、如果报依赖错误，输入：sudo apt-get install -f
3、自动解决依赖后再执行步骤1

另外需要注意的是：在登录的时候，如果输入密码时提示密码错误，请使用旁边的软件盘进行鼠标点击输入就能成功了。



==============华丽的分割线，下面版本已过时====================
1.下载Wine QQ安装包

WineQQ2013SP6-20140102-Longene

本帖软件包来自：http://www.longene.org/forum/vie ... 4700&p=12241#p12241,
2.具体安装

32位系统安装说明：

    1.如果之前安装过旧版本需要先卸载（通过dpkg -l | grep qq查看）。
    卸载: 先dpkg -l | grep qq 找到 名字xxx，然后执行：sudo dpkg -P  名字xxx
    2.安装: sudo dpkg -i 软件名.deb
    3.安装后qq在桌面上方dash中找到qq点击即可运行。
    4.安装后第一次运行qq登录的时候可能有点慢这是正常的，qq要生成自己的一些用户信息


64位系统安装说明：

    运行如下代码一次性解决所有依赖：sudo apt-get install libgtk2.0-0:i386
    然后再参考32位的安装方式

另外需要注意的是：在登录的时候，如果输入密码时提示密码错误，请使用旁边的软件盘进行鼠标点击输入就能成功了。（这应该是个BUG）   

