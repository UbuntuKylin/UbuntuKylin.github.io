---
title: '如何对Ubuntu Kylin 14.04 的登录界面截图 '
toc: true
date: 2019-06-29 11:50:34
tags:
categories:
---





## 每周一贴：如何对Ubuntu Kylin 14.04 的登录界面截图



有时用户需要对登录界面屏幕截图。例如，如果用户想写一篇有关如何在Ubuntu Kylin 14.04 上安装Cinnamon 的技术文章，登陆界面的截图就对初学者有帮助。无论你的原因是什么，如果你想知道如何对Ubuntu  Kylin 14.04 或Linux Mint 17 的登陆界面截图，让下面的技巧来告诉你怎么做吧。

对Ubuntu Kylin和Linux Mint的登录界面截图

这里的方法是创建一个可以从命令行界面运行的脚本，不要害怕这个脚本，使用它真的很简单。

第1步：获取ImageMagic

打开终端，然后使用以下命令安装ImageMagic。

sudo apt-get install imagemagick

第2步：准备脚本

创建一个新的文件，最好在你的home目录下，将它命名为screenshot.sh或任何你喜欢的。在文件中添加以下几行： 
chvt 7; sleep 5s; DISPLAY=:0 XAUTHORITY=/var/run/lightdm/root/:0 xwd -root -out ~/screenshot.xwd; convert ~/screenshot.xwd ~/screenshot.png; rm ~/screenshot.xwd

在上述中，chvt 7是虚拟控制台的数量。当你运行这个脚本后需要5秒来截图，你可以把它改成任何你想要的数字，会发现命名为screenshot.png的截图保存在你的home目录下。

第3步：给脚本执行权限

你必须要给脚本执行权限：

sudo chmod +x screenshot.sh

第4步：截图

现在，当一切准备就绪后，退出系统。进入用户登录模式后按Ctrl+Alt+F1，输入你的用户认证，然后像这样运行截图脚本：

sudo ./screenshot.sh

一旦这个脚本运行时，它会带你回到登录界面的图形界面（chvt 7），五秒钟后文件名为screenshot.png的截图将会保存在你的home目录下。

你可以根据自己的需要修改截图脚本。希望这个技巧能帮你对Ubuntu Kylin、Linux Mint或任何其他的Linux发行版的登录界面进行截图。如果你有任何疑问或建议，随时欢迎与我们UK团队联系。
