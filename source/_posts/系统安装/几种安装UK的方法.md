---
title: 几种安装UK的方法
toc: true
date: 2019-05-17 14:13:21
tags:
categories:
---





## 几种安装UK的方法   
近几日UbuntuKylin13.04 Beta发布，而UbuntuKylin13.04正式版也将在4月25日发布，随着“更有中国味的操作系统”的宣传，现在越来越多的人怀着好奇之心跃跃欲试，也有很多人在真正上手的时候发现安装遇到了一些问题。所以，本菜鸟就斗胆整理列举一些安装方式。   
首先，UbuntuKylin至少暂时不能良好支持wubi安装这种方式，虽然很多人都知道它提供了在现有Windows系统下像安装软件一样划区安装Ubuntu，但是由于种种原因，这种方式不能适用UbuntuKylin。所以，不建议使用这种方式直接安装UbuntuKylin。   
UbuntuKylin的安装体验有以下多种方式，具体分为3类：   
一，虚拟安装   
二，硬盘安装，包括实现多系统共存（4G以上U盘也是可以安装的，本质相同，但需要注意不同点，参见《将UbuntuKylin安装到U盘》http://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=180）
UbuntuKylin实质安装阶段可参见
@tao61的帖子《UbuntuKylin体验记》[点击此处](http://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=153)和
@bunny《UbuntuKylin安装步骤图解》[点击此处](http://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=147)预览  
关于32位（i386）和64 位（amd64）系统的选择：
       如果你的机器预装的是Windows 8系统，请安装64位系统；
       即使新型机器不是预装Windows 8，很多都是64位CPU，自己选择32位或者64位系统，请注意32位不能兼容4G及以上内存，需要安装pae内核（一说现在Ubuntu默认内置的就是兼容内核，支持大于4G的内存）。
      
关于Windows下的UbuntuKylin系统启动引导项的问题：
       由于Windows系统不能自动加载Linux系统引导项及其加载器，若不把UbuntuKylin的引导加载器grub2装到主引导记录MBR上，你就需要手动添加引导项，这里列举两款软件，具体教程还请移步《Windows下添加UbuntuKylin引导教程》[点击此处](
http://www.ubuntukylin.com/ukyli ... =viewthread&tid=382）
      1）用EasyBCD，据说需要安装1.7以上版本，个人免费版就够，因为一些引导可能出现的问题，建议安装到非系统盘。
      2）用Grub4Dos，需要最新版[点击此处](http://download.gna.org/grub4dos/grub4dos-0.4.4-2009-06-20.zip)

另外，由于本人精力及能力有限，难免有疏漏之处甚至严重错误出现，敬请诸位不吝斧正。
3L的帖子因“某些信息不法”无法再编辑，特此顶楼更正：dd烧录命令有误，应是$ dd if=/dev/sdb1 of=PATH_TO_ISO（ISO路径，如/home/ubuntu-13.04-desktop-amd64.iso）

另：Android手机借助应用DriveDroid也可以实现引导硬盘安装UbuntuKylin，参见@USER《丢掉U盘，用drivedroid装麒麟》[点击此处](http://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=412)

帖子发布不久，就看见驱动之家的帖子《再见Wubi：Ubuntu不再支持从Windows安装》[点击此处](http://news.mydrivers.com/1/259/259231.htm)，所以wubi安装UbuntuKylin的最后一点希望也破灭了。  
感谢@牛精kk提出建设性建议：清明期间更新了Linux系统下安装UbuntuKylin的方法；
       我想应该没有多少果粉要在Mac上安装Linux，Mac OS也属于Unix，如此“不折腾不舒服斯基”和“不折腾会死星人”应该也不需要看这帖子了。
