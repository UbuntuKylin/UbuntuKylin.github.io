---
title: 10个 Adobe 风格的创意图标，你值得拥有！
toc: true
date: 2019-06-24 09:06:07
tags:
categories:
---





## 10个 Adobe 风格的创意图标，你值得拥有！

我知道，在开源的世界里，Adobe 是个让人闻风丧胆的词。当然，我今天不是要给你推荐 Adobe 公司的任何产品，而是其他。

你肯定注意到了，Adobe 公司推出的所有产品图标都是两个单词放在上面。非常的朴实、简单，却不失优雅。在这里，设计师 ROhit Awate 就为一些开源的应用软件（ 如 Gimp 和 Krita ）设计了几个相似的图标。 

事实上，在四月份的时候，Rohit 就已经把这两个图标发布，他因此得到很多好的反馈。所以，他又为另外8个开源应用设计了相似风格的图标。以下，是目前图标组中的软件：Gimp、Inkscape、Krita、Darktable、Ardour、Audacity、OpenShot、Kdenlive、Blender、Scribus。

![](http://www.ubuntukylin.com/upload/201608/1470636139204717.jpg) 

使用这些图标，并不像直接使用 Ubuntu Kylin 中的图标主题那样。它不会自动变，你需要手动的编辑每个应用的文件，从而得到新图标。这并不是很难哟，相信你可以很轻易完成的！ 

用命令行来编辑应用的文件，工作量不大也并不难。但是呢，为了 Ubuntu Kylin 的初学者着想，我展示一下在图形界面要怎么设置吧。 

在 Ubuntu Kylin 中使用 Adobe 风格的图标 

下面就是如何得到 Adobe 风格图标的步骤：

步骤一：从网址[点击此处](http://rohitawate.deviantart.com/art/The-Adobe-Icons-Project-600489814)得到图标。

下载压缩包，解压之后就可以看到用图标命名的文件夹。注意要把文件夹复制在一个你不会和别的文件弄混淆的地方。因为如果你不小心把图标文件夹删除，你的应用就会丢失图标，你可不想这样吧。 

步骤二：进入“计算机->usr->share->applications”，找到你想要改变图标的应用软件，这里用 Gimp 举例：

![](http://www.ubuntukylin.com/upload/201608/1470636222321372.jpg) 

步骤三：右键 GIMP ，选择“复制”，成功复制 Gimp.desktop 文件的路径。 

![](http://www.ubuntukylin.com/upload/201608/1470636273530817.jpg)

步骤四：打开终端，运行命令。

![](http://www.ubuntukylin.com/upload/201608/1470636409218075.jpg) 

步骤五：在这个 gimp.desktop 文件中，找到由 Icon 开头的那一行。 

![](http://www.ubuntukylin.com/upload/201608/1470636601154274.jpg) 

步骤六：进入存放图标的文件夹，右键点击你想要的图标，选择“复制”。这一步就相当于复制这个图标的路径。 

![](http://www.ubuntukylin.com/upload/201608/1470636485588784.jpg) 

步骤七：回到已打开的 gimp.desktop，把复制好的图标路径放入文件如图所示位置。

![](http://www.ubuntukylin.com/upload/201608/1470636428935951.jpg)  

最后，点击“保存”。注销，再登入，你就会发现图标已经替换，同样在 dash 里也变了。 

![](http://www.ubuntukylin.com/upload/201608/1470636808424141.jpg)
