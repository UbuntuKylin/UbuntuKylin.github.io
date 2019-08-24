---
title: 如何制作Ubuntu/Ubuntu Kylin SDK Live USB盘
toc: true
date: 2019-06-24 09:14:29
tags:
categories:
---





## 每周一贴：如何制作Ubuntu/Ubuntu Kylin SDK Live USB盘

    原文来自：Ubuntu 应用开发培训教程专栏

    对于一些想开发Ubuntu手机应用或Scope的开发者来说，不想重新买一个电脑安装Ubuntu操作系统或在自己的硬盘上重新安装一个Ubuntu系统，那么可以考虑制作一个Ubuntu系统的Live USB盘。这个USB包括如下的部分：

    Ubuntu Kylin 14.10操作系统
    Ubuntu SDK （包括已经安装好的SDK，模拟器及编译环境）

    使用这个Live USB盘，开发者就不用安装任何的东西，直接插入电脑的USB口中。在电脑启动的过程中，选择我们制作好的USB启动盘进行启动（在电脑启动的过程中，按下“F12”键）。在启动的过程中选择“Try Ubuntu Kylin without installing”   优麒麟（Ubuntu Kylin）

    虽然这是一个Ubuntu OS的启动盘，但是它可以保存我们在开发过程中所创建的项目(存于Home目录中）及一些设置（比如wifi设置密码等）。

    当我们选择USB时，我们最好是选择USB 3.0并把USB盘放入到电脑USB 3.0的口中。一般来说，电脑上的USB 3.0口是用蓝色标示的。建议使用质量较好，速度较快一点的USB这样可以使得系统的启动和运行更快更流畅。目前我们使用SanDisk CZ80来做测试，效果还是不错的。USB需要有16G的存储。

    为了使得我们的模拟器能够更加流畅及模拟器不会出现黑色的屏幕，我们需要在电脑的BIOS里启动硬件虚拟化功能。开发者需要到自己的电脑的BIOS里的设置启动VT-X/AMD-V。开发者可以参考文章“Ubuntu SDK 安装”来检查自己的电脑是否支持virtualization。

    如果开发者想要在自己的电脑上安装Ubuntu系统并在上面开发的话，可以参考文章“Ubuntu SDK 安装”来一步一步地安装Ubuntu SDK。   优麒麟（Ubuntu Kylin）
１）如何在Ubuntu系统下制作Live USB盘

    启动Ubuntu操作系统，打开浏览器并在如下的地址下载最新的image:  ttps://mega.co.nz/#F!S8QSRZyI!2HBWgXk4kmc_2bcCcpBR3Q

    下载的文件包含：

    kylin-live-20150133.iso (md5sum 13cd61270bf98eb462dc0497df8eee33)
    casper-rw-20150113.tar.bz2  (md5sum 8c69f94a03481275bf66aa883b69ae1b)
    post-usb-creator-window.sh（在Windows下制作需要这个）
    README.md （简单的说明文件）

    我们把下载的文件存于到我们想要的一个目录中，比如在自己的Home下的“usb”目录中。

在Dash中输入“usb”，并启动“Startup Disk Creator/启动盘创建器”    优麒麟（Ubuntu Kylin）    优麒麟（Ubuntu Kylin）

    我们按照如下的方法来制作我们的USB启动盘。
优麒麟（Ubuntu Kylin）

优麒麟（Ubuntu Kylin）

    在设置“储存在额外保留空间”时，它的值应该为非零的值。等USB盘已经制作好以后，你将会看到如下的画面：

优麒麟（Ubuntu Kylin）优麒麟（Ubuntu Kylin）

    重新挂载USB盘，因为在前一步会自动卸载USB盘，或者在Ubuntu中的文件浏览器中点击USB所在的device。这样就可以完成重新挂载USB：优麒麟（Ubuntu Kylin）

优麒麟（Ubuntu Kylin）

    然后按下面运行自带的脚本，参数为 USB 盘挂载的路径。
解压已经下载的casper-rw-2015xxxx.tar.bz2文件

    等文件都被解压完后，进入解压文件所在的目录，并在shell中执行如下的指令：
    liuxg@liuxg:~/usb$ ./post-usb-creator-linux.sh /media/liuxg/BD52-7153/
    这里“/liuxg/BD52-7153”为USB盘挂载的路径。根据自己USB盘所在的路径替换。
2）如何在Windows 平台下制作启动盘
http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows

    下载制作工具，与 Linux 平台的工具相似。

优麒麟（Ubuntu Kylin）

    单我们在选择“Persistent file”时，它的大小应该是非零的一个值。在我们填入“Step 2”时，我们不应该把拷贝好的字符串拷到该输入框中，否则在“Step 3”中的输入框就会是灰色的。我们应该点击“Browse”按钮，并按照如下的方式进行输入image的路径：

优麒麟（Ubuntu Kylin）

    在这之后把 casper-rw 文件拷贝到USB的主目录下即可。

    注：如果只想使用英文版的Ubuntu系统就不需要进行下面的步骤。如果想要支持中文版，请把 post-usb-creator-window.sh 也拷贝到 USB盘的根目录下。从USB 盘启动Ubuntu系统后，在shell中执行如下的指令：

    $ cd /cdrom/
    $ sudo ./post-usb-creator-window.sh

    再次重新启动后，会进入中文版的Ubuntu系统。
3）测试已经制作好的USB启动盘

    我们可以把我们的Live USB盘插入电脑，我们可以通文章“创建第一个Ubuntu for phone应用”来检验我们是否有一个完好的Ubuntu SDK。

    在我们启动模拟器时，如果需要输入密码，请使用默认的密码“0000”。如果开发者需要自己修改这个密码，请到Ubuntu SDK模拟器中的“系统设置”中去修改。

    对于应用开发者来说，在Qt Creator中的热键组合“Ctrl + Space”键有它独特的用处。可是，在Ubuntu系统中，“Ctrl + Space”被用来转换中英文输入法。建议开发者参考文章“怎么在Ubuntu OS上面安装搜狗输入法及对Qt Creator的支持”来重新定义键的组合。
已知问题 (known issues)

    如果你在使用的过程中，发现有如下的乱码的情况（极少情况下出现），请重新启动你的机器来纠正这个问题。

优麒麟（Ubuntu Kylin） 

在个别电脑上不能启动的问题

    我们发现在联想 E455 出现不能启动的问题，目前怀疑是和 AMD 显卡驱动有关，问题仍在调查中，如果遇到些问题，请在系统上安装14.04 LTS版本并安装相应的ubuntu-sdk包来尝试学习ubuntu phone的开发知识，其中的基本概念都是一样。

    注：如果想长时间致力于ubuntu phone的开发建议在电脑上安装一个ubuntu系统，最好是utopic (14.10)，而不是在Live环境下进行学习，一是以防数据的丢失，二是在使用性能上有更快速的体验。

 