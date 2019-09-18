---
title: 如何使用Aptik来备份和恢复 Ubuntu/Ubuntu Kylin 中的Apps和PPAs
toc: true
date: 2019-06-24 14:30:22
tags:
categories:
---


<img src="http://www.ubuntukylin.com/upload/images/a1(1).png"></img>

当你想重装Ubuntu/Ubuntu Kylin或者仅仅是想安装它的一个新版本的时候，如果有个便捷的方法来重新安装之前的应用并且重置其设置会很方便的。此时 Aptik 粉墨登场，它可以帮助你轻松实现。

**Aptik**（自动包备份和恢复）是一个可以用在Ubuntu、Ubuntu Kylin 和其他基于Debian以及Ubuntu的Linux发行版上的应用，它允许你将已经安装过的包括软件库、下载包、安装的应用和主题、用户设置在内的PPAs(个人软件包存档)备份到外部的U盘、网络存储或者类似于Dropbox的云服务上。

注意：当我们在此文章中说到输入某些东西的时候，如果被输入的内容被引号包裹，请不要将引号一起输入进去，除非我们有特殊说明。

想要安装Aptik，需要先添加其PPA。使用Ctrl + Alt + T快捷键打开一个新的终端窗口。输入以下文字，并按回车执行。

 * sudo apt-add-repository –y ppa:teejee2008/ppa

当提示输入密码的时候，输入你的密码然后按回车。

<img src="http://www.ubuntukylin.com/upload/images/a2(1).png"></img>

在命令行提示符输入下边的命令，来确保资源库已经是最新版本。

 * sudo apt-get update

![](http://www.ubuntukylin.com/upload/images/a3.png)

更新完毕后，你就完成了安装Aptik的准备工作。接下来输入以下命令并按回车：

 * sudo apt-get install aptik

注意：你可能会看到一些有关于获取不到包更新的错误提示。不过别担心，如果这些提示看起来跟下边图片中类似的话，你的Aptik的安装就没有任何问题。

![](http://www.ubuntukylin.com/upload/images/a4.png)

安装过程会被显示出来。其中一个被显示出来的消息会提到此次安装会使用掉多少磁盘空间，然后提示你是否要继续，按下“y”再按回车，继续安装。

![](http://www.ubuntukylin.com/upload/images/a5.png)

当安装完成后，输入“Exit”并按回车或者按下左上角的“X”按钮，关闭终端窗口。

![](http://www.ubuntukylin.com/upload/images/a6.png)

在正式运行Aptik前，你需要设置好备份目录到一个U盘、网络驱动器或者类似于Dropbox和Google Drive的云帐号上。这儿的例子中，我们使用的是Dropbox。

![](http://www.ubuntukylin.com/upload/images/a7.png)

一旦设置好备份目录，点击启动栏上方的“Search”按钮。

![](http://www.ubuntukylin.com/upload/images/a8.png)

在搜索框中键入 “aptik”。结果会随着你的输入显示出来。当Aptik图标显示出来的时候，点击它打开应用。

![](http://www.ubuntukylin.com/upload/images/a9.png)

此时一个对话框会显示出来要求你输入密码。输入你的密码并按“OK”按钮。

![](http://www.ubuntukylin.com/upload/images/a10.png)

Aptik的主窗口显示出来了。从“Backup Directory”下拉列表中选择“Other…”。这个操作允许你选择你已经建立好的备份目录。

注意：在下拉列表的右侧的 “Open” 按钮会在一个文件管理窗口中打开选择目录功能。

![](http://www.ubuntukylin.com/upload/images/a11.png)

在 “Backup Directory” 对话窗口中，定位到你的备份目录，然后按“Open”。

注意：如果此时你尚未建立备份目录或者想在备份目录中新建个子目录，你可以点“Create Folder”来新建目录。

![](http://www.ubuntukylin.com/upload/images/a12.png)

点击“Software Sources (PPAs).”右侧的 “Backup”来备份已安装的PPAs。

![](http://www.ubuntukylin.com/upload/images/a13.png)

然后“Backup Software Sources”对话窗口显示出来。已安装的包和对应的源（PPA）同时也显示出来了。选择你需要备份的源（PPAs），或者点“Select All”按钮选择所有源。

![](http://www.ubuntukylin.com/upload/images/a14.png)

点击 “Backup” 开始备份。

![](http://www.ubuntukylin.com/upload/images/a15.png)

备份完成后，一个提示你备份完成的对话窗口会蹦出来。点击 “OK” 关掉。

一个名为“ppa.list”的文件出现在了备份目录中。

![](http://www.ubuntukylin.com/upload/images/a16.png)

 

接下来，“Downloaded Packages (APT Cache)”的项目只对重装同样版本的Ubuntu有用处。它会备份下你系统缓存(/var/cache/apt/archives)中的包。如果你是升级系统的话，可以跳过这个条目，因为针对新系统的包会比现有系统缓存中的包更加新一些。

备份和恢复下载过的包，这可以在重装Ubuntu，并且重装包的时候节省时间和网络带宽。因为一旦你把这些包恢复到系统缓存中之后，他们可以重新被利用起来，这样下载过程就免了，包的安装会更加快捷。

如果你是重装相同版本的Ubuntu系统的话，点击 “Downloaded Packages (APT Cache)” 右侧的 “Backup” 按钮来备份系统缓存中的包。

注意：当你备份下载过的包的时候是没有二级对话框出现的。你系统缓存 (/var/cache/apt/archives) 中的包会被拷贝到备份目录下一个名叫 “archives” 的文件夹中，当整个过程完成后会出现一个对话框来告诉你备份已经完成。

![](http://www.ubuntukylin.com/upload/images/a17.png)

有一些包是你的Ubuntu发行版的一部分。因为安装Ubuntu系统的时候会自动安装它们，所以它们是不会被备份下来的。例如，火狐浏览器在Ubuntu和其他类似Linux发行版上都是默认被安装的，所以默认情况下，它不会被选择备份。

像[package for the Chrome web browser](http://www.howtogeek.com/203768)这种系统安装完后才安装的包或者包含 Aptik 的包会默认被选择上。这可以方便你备份这些后安装的包。

按照需要选择想要备份的包。点击 “Software Selections” 右侧的 “Backup” 按钮备份顶层包。

注意：依赖包不会出现在这个备份中。

![](http://www.ubuntukylin.com/upload/images/a18.png)

备份目录中出现了两个名为 “packages.list” 和“packages-installed.list” 的文件，并且会弹出一个通知你备份完成的对话框。点击 ”OK“关闭它。

注意：“packages-installed.list”文件包含了所有的包，而 “packages.list” 在包含了所有包的前提下还指出了那些包被选择上了。

![](http://www.ubuntukylin.com/upload/images/a19.png)

要备份已安装软件的设置的话，点击 Aptik 主界面 “Application Settings” 右侧的 “Backup” 按钮，选择你要备份的设置，点击“Backup”。

注意：如果你要选择所有设置，点击“Select All”按钮。

![](http://www.ubuntukylin.com/upload/images/a20.png)

被选择的配置文件统一被打包到一个名叫 “app-settings.tar.gz” 的文件中。

![](http://www.ubuntukylin.com/upload/images/a21.png)

当打包完成后，打包后的文件被拷贝到备份目录下，另外一个备份成功的对话框出现。点击“OK”关掉。

![](http://www.ubuntukylin.com/upload/images/a22.png)

放在 “/usr/share/themes” 目录的主题和放在 “/usr/share/icons” 目录的图标也可以备份。点击 “Themes and Icons” 右侧的 “Backup” 来进行此操作。“Backup Themes” 对话框默认选择了所有的主题和图标。你可以安装需要的、取消一些不要的，然后点击 “Backup” 进行备份。

![](http://www.ubuntukylin.com/upload/images/a23.png)

主题被打包拷贝到备份目录下的 “themes” 文件夹中，图标被打包拷贝到备份目录下的 “icons” 文件夹中。然后成功提示对话框出现，点击“OK”关闭它。

![](http://www.ubuntukylin.com/upload/images/a24.png)

一旦你完成了需要的备份，点击主界面左上角的“X”关闭 Aptik 。

![](http://www.ubuntukylin.com/upload/images/a25.png)

备份过的文件已存在于你选择的备份目录中，可以随时查看。

![](http://www.ubuntukylin.com/upload/images/a26.png)

当你重装Ubuntu/Ubuntu Kylin或者安装新版本后，在新的系统中安装 Aptik 并且将备份好的文件置于新系统中使用。运行 Aptik，并使用每个条目的 “Restore” 按钮来恢复你的软件源、应用、包、设置、主题以及图标。
