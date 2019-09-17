---
title: Linux新手大礼包：学习Linux你必须知道的那些事儿
toc: true
date: 2019-06-24 14:31:49
tags:
categories:
---

　
　　欢迎加入 Linux 的大家庭！对你来说，这可能还是一个陌生的领域，不过相信随着逐步深入的了解，你会喜欢上 Linux，喜欢上开源的！首先，让我们来看一下，Linux新手应该注意和了解哪些事情吧！

### 1. 认识几个大牛

Linus Torvalds
生于1969年12月28日的芬兰赫尔辛基市，拥有美国国籍。他是 Linux 内核的最早作者，随后发起了这个开源项目，担任 Linux 内核的首席架构师与项目协调者，是当今世界最著名的电脑程序员、黑客之一。他还发起了 Git 这个开源项目，并为主要的开发者。

Richard Matthew Stallman
简称 RMS，生于1953年3月16日，美国自由软件运动的精神领袖、GNU 计划 以及自由软件基金会的创立者。作为一个著名的黑客，他的主要成就包括Emacs及后来的 GNU Emacs，GNU C 编译器及GDB调试器。他所写作的GNU通用公共许可证是世上最广为采用的自由软件许可证，为Copyleft观念开拓出一条崭新的道路。

Eric Steven Raymond
生于1957年12月4日，程序员，《大教堂与市集》的作者、《新黑客词 典》（"Jargon File"）的维护人、著名黑客。作为《新黑客词典》的主要编撰人以及维护者，雷蒙很早就被认为是黑客文化的历史学家以及人类学家。但是在1997年以 后，雷蒙被广泛公认为是开放源代码运动的主要领导者之一，并且是最为大众所知道（并最具争议性）的黑客。

### 2. 了解Linux家族的明星成员
　　**Red Hat Enterprise Linux**：Red Hat Enterprise Linux 是 Red Hat 公司的 Linux 发行版，面向商业市场，包括大型机。红帽公司从 Red Hat Enterprise Linux 5 开始对企业版 LINUX 的每个版本提供10年的支持，Red Hat Enterprise Linux 常简作 RHEL。Red Hat Enterprise Linux 大约3年发布一个新版本。
　　**Fedora Linux**：Fedora Linux 是较具知名度的 Linux 发行版之一。它是一套功能完备、更新快速的免费操作系统。而对赞助者 Red Hat 公司而言，它是许多新技术的测试平台，被认为可用的技术最终会加入到 Red Hat Enterprise Linux 中。
　　**Centos**：CentOS 全名为“社区企业操作系统”（Community Enterprise Operating System），是Linux发布版之一，它是来自于 Red Hat Enterprise Linux 依照开放源代码规定发布的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以CentOS替代商业版的 Red Hat Enterprise Linux 使用。两者的不同，在于 CentOS 并不包含封闭源代码软件。CentOS 对上游代码的主要修改是为了卸载不能自由使用的商标。
　　**Ubuntu**：Ubuntu 是一个以桌面应用为主的 GNU/Linux 操作系统，其名称来自非洲南部祖鲁语或豪萨语的“ Ubuntu ”一词，意思是“人性”。 Ubuntu 基于 Debian 发行版，与 Debian 的不同在于它每6个月会发布一个新版本。
　　**SUSE Linux**：SUSE 是 Linux 操作系统其中一个发布版，也是德国的一个发布版。SUSE Linux 目前专注于企业市场。
　　**openSUSE**：openSUSE 是一个开放社区的计划，号称“最美丽的 Linux 发行版”。
　　**Debian**：Debian 是一种自由操作系统，全称 Debian GNU/Linux，由Debian计划（Debian Project）组织维护，Debian 是一个纯粹由自由软件所组合而成的操作环境。
　　**Archlinux**：Arch Linux(或称Arch)是一种以轻量简洁为设计理念的Linux发行版。其开发团队秉承简洁、优雅、正确和代码最小化的设计宗旨。Arch Linux 项目受 CRUX 启发，由 Judd Vinet 于2002年启动。

更多Linux版本请看这里： [Linux系统家族族谱](https://code.csdn.net/groups/7587/discources/935281)

### 3. 初学者必读的Linux基础书籍　　
　　要想学好Linux，你至少需要：一本好入门教材、一本linux指令参考手册、linux系统管理手册、讲解linux系统原理的书。这里我们推荐几部公认的好书：
 [《 鸟哥的Linux私房菜 基础学习篇》](http://book.douban.com/subject/4889838/) 鸟哥 著；人民邮电出版社
 [《 鸟哥的Linux私房菜 服务器架设篇》](http://book.douban.com/subject/10794788/)  鸟哥 著；机械工业出版社
 [《 Linux命令、编辑器与Shell编程》](http://book.douban.com/subject/25750712/) [美]索贝尔(Sobell·M.G.) 著； 清华大学出版社
 [《 Linux设备驱动程序》](http://book.douban.com/subject/1723151/) 科波特 著； 中国电力出版社
 [《 深入理解Linux内核》](http://book.douban.com/subject/2287506/) （美）博韦，西斯特 著； 中国电力出版社
 [《 UNIX环境高级编程》](http://book.douban.com/subject/1788421/)  W.Richard Stevens / Stephen A.Rago 著；人民邮电出版社

### 4. 熟悉Linux常用命令

 * man ：任何时候你觉得对一个命令行不是很确定，都可以通过输入“man + 命令”来了解这个命令能确切是做什么的。
 * ls ：列出目录内容。
 * pwd ：在终端中显示当前工作目录的全路径。
 * cd ：要变更你当前所在的目录。
 * mkdir ：创建一个新的目录。
 * cp ：复制文件/重命名文件。
 * mv ：移动文件。
 * find 和 locate：搜索文件。
 * kill ：快速关闭一个进程。
 * passwd ：更改密码。
 * md5sum ：计算和检验MD5信息签名
 * history ：查询历史记录命令。
 * sudo ：(super user do)命令允许授权用户执行超级用户或者其它用户的命令。
 * touch ：创建一个新文件，或者将文件的访问和修改时间更新为当前时间。
 * chmod ：修改文件的访问权限。
 * chown ：改变文件拥有者和所在用户组。
 * apt ：APT是一个为Debian系列系统（Ubuntu，Kubuntu等等）开发的高级包管理器，在Gnu/Linux系统上，它会为包自动智能地搜索、安装、升级以及解决依赖问题。

### 5. 小心新手常犯的几个错误　
　**不要以根用户登录**：这是使用Unix的惯例，除非必须那么不要轻易在根用户下运行任何东西。　
　**文件命名混乱**：避免使用美元符（$），括弧和百分号（%）等特殊字符，这些字符对于shell有着特殊意义，可能会引起冲突。避免使用空格，不要使用无效字符，“/”是根目录专用的。　
　**所有文件都混在一起**：将Home目录放在一个独立的分区上，可以在你重装系统甚至升级你的整个版本而不会丢失你的数据和个人设置。　
　**试图点击运行.exe文件**：除非你安装了WINE，双击那些.exe文件毫无用处。新用户需要知道，无论是Linux还是Windows，都只会运行针对自身系统开发的应用程序。　　
　**以默认格式向微软Office用户发送OpenOffice文档**：微软产品对其它操作系统和其它应用程序的友好性并不强，许多新Linux用户在共享文件给朋友时往往会遇到麻烦，因为对方无法阅读他们共享的文件格式，因此新Linux用户要注意存储文件的格式，确保它们能够被微软类似应用所打开。
　**忽视更新**：新的更新可以为一些新的漏洞打上补丁。维持更新可以在一个易受损的系统与一个安全的系统之间构造分水岭。Linux的安全来自于不断地维护。　　　　
　以上是一些操作习惯方面的错误，还有一些技术类型的错误，你可以查看《 避免UNIX和Linux中的常见错误》

### 6. 常去逛逛一些Linux社区和网站

国内的专业Linux网站
　　[ChinaUnix](http://www.chinaunix.net/)： 创办于2001年，是一个以讨论Linux/Unix类操作系统技术、软件开发技术、数据库技术和网络应用技术等为主的开源技术社区网站。 
　　[LinuxCN](http://linux.cn/)：Linux中国是专注于中文Linux技术、资讯的社区，在这里你可以获得一手的Linux资讯和技术知识。

国外著名Linux网站
　　[Linux Online](http://www.linux.org/)： 最权威的Linux网站，文章讨论无所不包，软件硬件应有尽有。
　　[Linux国际协会(Linux International)](http://li.org/)：有大量的Linux资源列表。
　　[Linux](http://www.linux.com/)：学习Linux的最好网站，也是Linux使用经验的汇聚地。
　　[Linuxforums](http://www.linuxforums.org/)： 提供Linux的软件资源，Linux论坛，Linux服务器发行版的信息，LINUX文章教程等信息的综合性网站。

