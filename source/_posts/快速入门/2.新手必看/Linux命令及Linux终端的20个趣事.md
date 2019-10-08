---
title: Linux命令及Linux终端的20个趣事
toc: true
date: 2019-06-24 09:15:34
tags:
categories:
---


玩Linux其乐无穷！哈哈。不相信。记住我的话，在文章结尾时你就会相信Linux确实好玩了。
![](https://www.ubuntukylin.com/upload/images/tl0.png)
### 命令：sl （蒸汽机车）
你可能了解 ‘ls’ 命令，并经常使用它来查看文件夹的内容。但是，有些时候你可能会拼写成 ‘sl’ ,这时我们应该如何获得一些乐趣而不是看见“command not found”呢？
安装 sl     
![](https://www.ubuntukylin.com/upload/images/tl1.png)
输出
![](https://www.ubuntukylin.com/upload/images/tl2.png) 
![](https://www.ubuntukylin.com/upload/images/t13.png)
当你敲入的是‘LS‘而不是’ls‘时，这个命令也会运行。

### 命令：telnet

非也！非也！！这可不像它平常那样复杂。你可能很熟悉telnet。Telnet 是一个文本化的双向网络协议。这里不需要安装什么东西。你需要的就是一个Linux系统和一个连通的网络。
![](https://www.ubuntukylin.com/upload/images/t14.png)
![](https://www.ubuntukylin.com/upload/images/tl5.png)

### 命令：fortune

试试你未知的运气，终端里有时也有好玩的。

安装 fortune
![](https://www.ubuntukylin.com/upload/images/tl6.png)

### 命令：rev（翻转）

它会把传递给它的的每个字符串都反过来，是不是很好玩。
![](https://www.ubuntukylin.com/upload/images/tl7.png)

### 命令：factor

该谈点儿关于Mathematics的了，这个命令输出给定数字的所有因子。

![](https://www.ubuntukylin.com/upload/images/tl8.png)

### 命令：script

好的，这不是什么命令，而是一个脚本，一个很有趣的脚本。

![](https://www.ubuntukylin.com/upload/images/tl9.png)

### 命令：Cowsay

一个在终端用ASCII码组成的小牛，这个小牛会说出你想要它说的话。

安装Cowsay
![](https://www.ubuntukylin.com/upload/images/tl10.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl11.png)

如果用管道将‘fortune command’命令重定向到cowsay会怎样呢？

root@tecmint:~# fortune | cowsay

![](https://www.ubuntukylin.com/upload/images/tl12.png)

提示：‘|’是管道命令符。通常它是将一个命令的输出作为下一个命令的输入。在上面的例子中‘fortune’的输出作为‘cowsay’命令的输出。管道命令会经常用在脚本和程序编写中。

xcowsay是一个图形界面程序。它与cowsay类似只是以一种图形的方式来表达，可以说是X版本的cowsay。

![](https://www.ubuntukylin.com/upload/images/tl13.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl14.png)

![](https://www.ubuntukylin.com/upload/images/tl15.png)

cowthink是另一个命令。运行“cowthink Linux is sooo funny ”看看它与cowsay的不同吧。
![](https://www.ubuntukylin.com/upload/images/tl16.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl17.png)

### 命令：yes

yes 是一个非常有趣又有用的命令，尤其对于脚本编写和系统管理员来说，它可以自动地生成预先定义的响应或者将其传到终端。

![](https://www.ubuntukylin.com/upload/images/tl18.png)

提示: (直到你按下ctrl+c才停止)

### 命令: toilet

什么？你在开玩笑吗! 当然没有，但肯定的是这个命令的名字太搞了，我也不知道这个命令的名字从何而来。

安装toilet

![](https://www.ubuntukylin.com/upload/images/tl19.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl20.png)

这个命令甚至提供了一些颜色和字体格式。

![](https://www.ubuntukylin.com/upload/images/tl21.png)

提示：Figlet 是另外一个与toilet产生的效果类似的命令。

### 命令：cmatrix

你可能看多好莱坞的电影‘黑客帝国’并陶醉于被赋予Neo的能看到在矩阵中任何事物的能力，或者你会想到一幅类似于‘Hacker’的桌面的生动画面。

安装 cmatrix

![](https://www.ubuntukylin.com/upload/images/tl23.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl24.png)

### 命令: oneko

可能你坚信Linux的鼠标指针永远是同样的黑色或白色一点儿也不生动，那你就错了。“oneko”是一个会让一个“Jerry”你的鼠标指针附着到你鼠标上的一个软件包。

安装 oneko

![](https://www.ubuntukylin.com/upload/images/tl25(1).png)

输出

![](https://www.ubuntukylin.com/upload/images/tl26.png)

![](https://www.ubuntukylin.com/upload/images/tl27.png)

提示：关闭运行着oneko的终端时，Jerry也会随之消失，重新启动终端时也不会再出项。你可以将这个程序添加到启动选项中然后继续使用它。

### Fork炸弹

这是一段非常欠抽的代码。运行这个命令的后果自己负责。这个命令其实是一个fork炸弹，它会以指数级的自乘，直到所有的系统资源都被利用了或者系统挂起（想要见识这个命令的威力你可以试一次这个命令，但是后果自负，记得在运行它之前关掉并保存其它所有程序和文件）。

![](https://www.ubuntukylin.com/upload/images/tl28.png)

### 命令：while

下面的”while“命令是一个脚本，这个脚本可以为你提供彩色的日期和文件直到你按下中断键（ctrl+c）。复制粘贴这个命令到你的终端。

![](https://www.ubuntukylin.com/upload/images/tl29.png)

![](https://www.ubuntukylin.com/upload/images/tl30.png)

提示：以上脚本通过下面的修改也会产生类似的输出但是还是有点不同的，在你的终端试试吧。

![](https://www.ubuntukylin.com/upload/images/tl31.png)

### 命令: espeak

将你的多媒体音箱的音量调到最大，然后在将这个命令复制到你的终端，来看看你听到上帝的声音时的反应吧。

安装 espeak

![](https://www.ubuntukylin.com/upload/images/tl32.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl33.png)

### 命令: aafire

在你的终端放一把火如何。把这个“aafire”敲到你的终端，不需要什么引号看看这神奇的一幕吧。按下任意键中指该程序。

安装 aafire

![](https://www.ubuntukylin.com/upload/images/tl34.png)

输出

![](https://www.ubuntukylin.com/upload/images/tl35.png)


![](https://www.ubuntukylin.com/upload/images/tl36.png)
### 命令: bb

首先安装“apt-get install bb”,然后敲入“bb”看看会发生什么吧。

![](https://www.ubuntukylin.com/upload/images/tl37.png)

![](https://www.ubuntukylin.com/upload/images/tl38.png)

### 命令: url

如果在你的朋友面前用命令行来改变你的 twitter status 会不会很酷呢。用你的用户名密码和你想要的状态分别替换username, password 和“your status message“就可以了。

![](https://www.ubuntukylin.com/upload/images/tl39.png)

### ASCIIquarium

想要在终端弄一个水族馆该，怎么办？

![](https://www.ubuntukylin.com/upload/images/tl40.png)

### 安装 ASCIIquarium

下载并安装ASCIIquarium。

![](https://www.ubuntukylin.com/upload/images/tl41.png)

最后在终端运行“asciiquarium”或者“/usr/local/bin/asciiquarium”，记得不要加引号，神奇的一幕将在你眼前展现。

![](https://www.ubuntukylin.com/upload/images/tl42.png)

![](https://www.ubuntukylin.com/upload/images/tl43.png)
### 命令: funny manpages
首先安装“apt-get install funny－manpages”然后运行下面命令的man手册。其中一些

![](https://www.ubuntukylin.com/upload/images/tl44.png)

### Linux Tweaks
该到了做一些优化的时候了

![](https://www.ubuntukylin.com/upload/images/tl45.png)

Linux总是sexy：who | grep -i blonde | date; cd ~; unzip; touch; strip; finger; mount; gasp; yes; uptime; umount; sleep（如果你知道我的意思，汗！）

还有一些其它的命令，只是这些命令并不能在所有的系统上运行，所以本文没有涉及到。比如说dog , filter, banner

使用愉快，你可以稍后再对我说谢谢：）

