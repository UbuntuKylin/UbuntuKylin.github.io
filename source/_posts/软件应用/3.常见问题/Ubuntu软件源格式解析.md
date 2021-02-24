---
title: Ubuntu软件源格式解析
toc: true
date: 2021-02-20 14:08:43
tags:
categories:
---
1. Ubuntu的包管理工具是apt，由于官方的软件源一般都在国外所以有时候源会很慢，所以有时候会替换成国内的镜像站，但是需要我们修改软件仓库的配置。Ubuntu的软件软分为两部分官方源和ppa，ppa其实是一个网站，即－launchpad.net。Launchpad 是 Ubuntu 母公司 Canonical 有限公司所架设的网站，是一个提供维护、支援或联络 Ubuntu 开发者的平台。由于不是所有的软件都能进入 Ubuntu 的官方的软件库，launchpad.net 提供了 PPA，允许开发者建立自己的软件仓库，自由的上传软件。供用户安装和查看更新。官方的源在/etc/apt/sources.list,ppa在/etc/apt/sources.list.d/这个文件夹里,我们说的换源是换的官方源,打开官方源的文件能看到很多链接.

deb http://mirrors.aliyun.com/ubuntu/       xenial main restricted universe multiverse

deb-src  http://mirrors.aliyun.com/ubuntu/      xenial main restricted universe multiverse


整个软件源结构可以分解为四个部分:
第一部分	    第二部分	                            第三部分	                                                        第四部分
软件包格式	    软件包服务器地址	                      发行版版本代号	软件包的分类目录
deb/deb-src	  http://mirrors.aliyun.com/ubuntu/ 	xenial/xenial-updates/xenial-security/xenial-backports/proposed	    main、restricted、universe、multiverse

2. 第一部分的deb是deb软件包，deb-src则是源代码包

第三部分严格来说不算是发行版版本代号，它应该是Ubuntu系统发布之后，在此基础上进行的安全性更新的分类。

第四部分是按照软件包的自由度来分类的：

main：即“基本”组件，其中只包含符合Ubuntu的协议要求并由Ubuntu团队维护支持的软件。

restricted：即“受限”组件，其中包含了非常重要的，但并不具有合适的自由协议的软件，如显卡驱动，同样有 Ubuntu团队维护支持。

universe：即“社区维护”组件，其中包含的软件种类繁多，它们可能采用受限于协议，可能不是，但都不为Ubuntu 团队维护。

multiverse：即“非自由”组件，其中包括了不符合自由软体要求而且不被Ubuntu团队支援的软件，通常为商业公司编写的软件。

3. 下面我们来看一下Ubuntu软件源镜像站的目录结构（以阿里云镜像站为例）： http://mirrors.aliyun.com/ubuntu/ ，在浏览器地址栏中输入此地址便进入了Ubuntu软件源镜像站，如下图所示：[图1] (https://www.ubuntukylin.com/ukylin/data/attachment/forum/201912/27/151031uvap21lg32epp0zo.png)

重点看两个文件夹dists和pool

dists目录包含的全是Ubuntu发行版目录及其附加仓库目录（如：xenial、xenial-update、xenial-security、xenial-backports就是Ubuntu xenial发行版目录及其附加仓库目录）。

pool/:

所有 Ubuntu 发布版及已发布版的软件包的物理地址。按照源码包名称分类存放。pool目录下按属性再分类（main、restricted、 universe和multiverse），分类下面再按源码包名称的首字母归档。这些目录包含的文件有：运行于各种系统架构的二进制软件包，生成这些二进制软件包的源码包。  

我们知道Ubuntu还有其他的附加仓库，Ubuntu附加仓库的命名格式是“版本代号-限定词”，限定词是这update、security、proposed、backports四个词中的一个，比方说版本代号xenial和限定词update组合就是xenial-update附加仓库，xenial和security组合就是xenial-security附加仓库，以此类推可以自行写出Ubuntu所有的附加仓库的目录名称。

4. 在sources.list文件里只有一条包含发行版仓库xenial的软件源还不够，我们还要写出包含其他4个附加仓库的软件源，只要把已经写好的软件源中的xenial依次替换成xenial-update、xenial-security、xenial-proposed、xenial-backports即可，下面是完整的包含所有附加仓库的软件源：

deb http://mirrors.aliyun.com/ubuntu/ xenial-update main universe restricted multiverse

deb http://mirrors.aliyun.com/ubuntu/ xenial-security main universe restricted multiverse

deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main universe restricted multiverse

deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main universe restricted multiverse

将这四条软件源再一并写入sources.list，再加上

deb http://mirrors.aliyun.com/ubuntu/ xenial main universe restricted multiverse

总共五条

另外为了防止运营商劫持大家可以使用https，但是要求镜像站支持https，一般现在大型镜像站都是支持https的，比如清华镜像站，阿里镜像站，163等。

本文在撰写过程中参考了以下文章
[https://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=191480](https://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=191480)

