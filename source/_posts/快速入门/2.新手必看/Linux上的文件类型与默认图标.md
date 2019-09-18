---
title: Linux上的文件类型与默认图标
toc: true
date: 2019-06-24 09:01:53
tags:
categories:
---





## Linux上的文件类型与默认图标

**引言**

也许小伙伴们对 Linux 已经有一定程度的了解，或者已经是一名能够在工作和生活中活用它的 Linux 用户了。随着桌面环境的不断发展，Linux 系统已经不再仅仅是一个面向极客和开发者的操作系统了，在 PC 上，上手 Linux 桌面已经可以变得像上手Windows 桌面一样简单。

本篇文章是一篇纯黑的技术软文，讲的是我们平时一般不会在意的东西，而且不会涉及具体编程方面的知识，所以小伙伴们不用担心文章过于晦涩难懂，尽情的一边喝茶一边涨知识吧！

### Windows上的文件类型与默认图标

在Windows上，文件类型基于唯一后缀名进行区分，比如——文本类型的后缀名是”.txt”，而Win32应用程序的后缀名是“.exe”。在win10系统中，这些后缀名默认被隐藏，在文件管理器的选项中更改设置为显示，就能够看到每个文件的后缀名了。

对于每一种文件类型，Windows上都有一个默认图标（一般exe的图标不是默认的，而是应用自己定制的），它的默认图标可以由默认打开它的应用决定，比如——使用winrar作为默认应用打开”.zip”压缩文件，那么所有的”.zip”类型文件默认图标都会变成winrar的图标；而使用2345好压作为默认打开应用，默认图标又会改变。

### Linux与Windows并不完全相同

在Linux系统上，有一些文件没有后缀名，比如Linux上的文本文件，即使不加txt后缀，一样的能够作为文本文件存在并被正确地显示和打开。

我们右键文本文件图标，打开属性窗口，可以看到“类型”： 

![](http://www.ubuntukylin.com/upload/201812/1544597804892983.png)

我们可以推测：默认图标的显示是与这个类型属性相关的。

### 让我们做一个实验

为了验证这个结论，我们需要做一个小实验。
 * 实验系统：Ubuntu Kylin 18.10
 * 实验对象：doc、docx类型文件
 * 实验方法：安装/卸载wps

也许大家没有注意过，在安装或者卸载了系统上的wps以后，doc和docx等类型文件的默认图标也改变了（如果没有，刷新或者重启一下）。

一般从优麒麟官网上下载的增强版自带了wps，我们打开一个目录，创建一个doc和docx文档： 

![](http://www.ubuntukylin.com/upload/201812/1544597909746823.png)

打开属性窗口： 
![](http://www.ubuntukylin.com/upload/201812/1544600648905345.png)

![](http://www.ubuntukylin.com/upload/201812/1544600648593032.png)

可以看到它们的文件类型，那么接下来我们打开终端（Ctrl+Alt+T），输入：

sudo apt remove wps-office 

![](http://www.ubuntukylin.com/upload/201812/1544600689772744.png)

![](http://www.ubuntukylin.com/upload/201812/1544600727686021.png)

卸载wps，接下来回到刚才创建的doc和docx所在的目录，刷新一下：

![](http://www.ubuntukylin.com/upload/201812/1544600745317428.png)

这个时候的默认图标类型已经变了，接着再打开属性： 

![](http://www.ubuntukylin.com/upload/201812/1544600761749681.png)

![](http://www.ubuntukylin.com/upload/201812/1544600786228952.png)

同样的文件，文件类型改变的同时图标也跟着改变，所以，之前所提出的推论是对的。 

那么，我们在安装/卸载wps的时候，它究竟做了什么？

### MIME-Info database

我们可以看到，在卸载wps的时候，出现了一些mime相关的配置，事实上，Linux上的文件类型标准就是这个MIME-Info database，所有文件类型相关的配置，包括默认图标，都是在这个database中定义的。

大家如果有兴趣，可以参考：[点击此处](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.18.html)

‘/usr/share/mime/packages’目录下存放着相关配置文件，其中freedesktop.org.xml 是 Linux 默认的文件类型基准。在这里，我们先找到 wps-office-wps.xml，并打开： 

![](http://www.ubuntukylin.com/upload/201812/1544600831986186.png)

其中，comment、mime-type就是属性窗口中的文件类型；

alias type，顾名思义，是mime-type的别名，所以这些文件类型就被wps-office.doc覆盖了；

generic-icon name，即文件类型的默认图标名；

glob partten，如果文件名中有匹配，则认为是该类型。

在/usr/share/icons目录下存放着默认图标： 

![](http://www.ubuntukylin.com/upload/201812/1544600848817269.png)

Linux的判断文件类型的最优先基准往往是通过文件名中的字段，如果字段和MIME-database匹配，则认为是该文件类型。然而，并非所有文件类型都规定了匹配字段，它们依旧能够确定类型，但是如果重命名后包含了MIME-database的匹配字段，则会优先使用对应类型覆盖原有的类型。

实际上，在之前举出的本文件创建的例子中，不需要后缀名的原因是文本类型的文件在创建的时候已经被赋予了MIME type，只要文件名不与其它MIME type的基准冲突，这个文本文件就能正常的显示和打开。

### DIY一个文件类型的图标

小伙伴们也许现在还有点一头雾水，没关系，接下来的干货才是重头戏；前面的看不懂？没关系，自己动手做一次，马上就理解了。

![](http://www.ubuntukylin.com/upload/201812/1544600873149787.png)

可以看到，命名为.so的文件的默认图标已经被小编改成了自己的图案，那么究竟是怎么做到的呢？接下来我们一步一步的完成。

**1、准备图标**

首先，我们需要准备自己的文件类型图片，一般使用png格式即可，文件图标可以在网上下载自己喜欢的，也可以使用GIMP自己绘制然后导出，小编这里为了方便，就自己简单的画了一下。GIMP可以在开始菜单中搜索gimp得到：

![](http://www.ubuntukylin.com/upload/201812/1544600900397307.png)

![](http://www.ubuntukylin.com/upload/201812/1544600900866148.png)

关于GIMP的使用，小编也是小白所以就不罗嗦了，大家有兴趣的话自行百度一下吧。

我们打开/usr/share/icons/ukui-icon-theme目录:

![](http://www.ubuntukylin.com/upload/201812/1544604859921343.png)

我们把准备好的图标放进对应尺寸文件夹的mimetypes目录下，比如48x48的png放到/usr/share/icons/ukui-icon-theme/48x48/mimetypes目录下。

由于在/usr/share目录下操作需要管理员权限，所以建议以管理员身分运行文件管理器，优麒麟18.10上，在终端输入：

sudo peony

就可以以管理员身分运行文件管理器，当然小伙伴们也可以使用sudo cp在终端操作。

还有，这里一定要注意，我们不同尺寸目录下的图标文件名必须一样，不然等会儿图片会找不全。

**2、编写自己的配置文件**

就像wps做的那样，我们也需要自己写一个.xml文件来覆盖原有的文件类型，这同样需要管理员权限。

我们在/usr/share/mime/packages目录下创建一个文本文件，命名为XXX.xml（这里小编的是sharedlib.xml），输入以下内容。

![](http://www.ubuntukylin.com/upload/201812/1544603156648367.png) 

最关键的是alias type、generic-icon name和glob pattern三项。保存退出。 

![](http://www.ubuntukylin.com/upload/201812/1544601011883301.png)

**3、更新**

现在我们的.so文件还没有变，因为我们还需要手动更新它。

依次执行：

sudo gtk-update-icon-cache /usr/share/icons/ukui-icon-theme/

sudo update-mime-database -V /usr/share/mime

第一条命令将我们的自定图片更新到cache中，使得文件管理器能够通过cache找到我们的icon；

第二条命令将我们对配置的更改更新至MIME-database中，这样我们的自定义配置就生效了。

我们刷新一下在看看，.so文件是不是变了？打开.so文件的属性，发现它的内容和mime-type也已经变成了我们自己写的类型。

也许有小伙伴们会问，为什么只有.so文件变了，.so.1.2.3之类的文件没有变呢？这就是glob参数的作用了，大家有兴趣可以研究一下freedesktop.org.xml文件，里面有对于application/x-sharedlib原来glob的标注，不光是.so，也能够识别类似.so.1.2.3的类型。

不知到大家是否有所收获呢？本篇文章虽然没有涉及代码编程，但是不同的人看，一定会有不同的体会和收获吧，在行文中小编凸显了一些细节，也略写了一些细节，希望大家看完这篇软文以后能够有所精进，让我们在Linux的道路上共同进步吧。
