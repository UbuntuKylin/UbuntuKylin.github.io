---
title: 有趣的Linux彩蛋——用sudo来冒犯用户
toc: true
date: 2019-06-24 14:26:59
tags:
categories:
---





## 有趣的Linux彩蛋——用sudo来冒犯用户

人们可以配置 sudo（用来给命令授权的），来冒犯那些输错密码的用户。一起来看看吧！

首先，打开终端，输入以下命令：

**sudo visudo**

强烈推荐使用 visudo 编辑 /etc/sudoers 配置文件。之所以使用 visudo 有两个原因，一是它能够防止两个用户同时修改它；二是，它可以帮助校验修改是否正确。visudo不会擅自保存带有语法错误的配置文件，它会提示你出现的问题，并询问该如何处理。visudo 默认的是在vi里打开配置文件，而在 Ubuntu Kylin 中，visudo 默认在 nano 中打开 /etc/sudoers。

然后，在文件顶部，加上这么一行：

**Defaults insults**

如图所示：　　

![](http://www.ubuntukylin.com/upload/201602/1456191668463393.jpg)

接下来，保存并且关闭文件。如果您使用的是nano，按Ctrl+X退出，它会提示您是否想要保存更改。请按Y保存更改。

然后，终端输入sudo -k，清空密码的缓存。最后，在sudo命令里输入错的密码：

![](http://www.ubuntukylin.com/upload/201602/1456192456272768.jpg)

看看，它还对我不耐烦呢。现在你也可以向朋友哭诉自家的sudo欺负你了^_^。