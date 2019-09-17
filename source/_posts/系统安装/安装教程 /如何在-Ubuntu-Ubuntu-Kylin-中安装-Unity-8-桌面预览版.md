---
title: 如何在 Ubuntu/Ubuntu Kylin 中安装 Unity 8 桌面预览版
toc: true
date: 2019-06-24 14:28:18
tags:
categories:
---


![](http://www.ubuntukylin.com/upload/images/unity8.jpg)

如果你一直在关注新闻，那么就知道 Ubuntu/Ubuntu Kylin 将会切换到带有 Unity 8 桌面的Mir显示服务器。然而，在尚未确定运行在Mir上的 Unity 8 是否会出现在 Ubuntu 15.10 willy werewolf 之前，有了一个 Unity 8 的预览版本可供你体验和测试。通过官方PPA，可以很容易地在 Ubuntu/Ubuntu Kylin 14.04，14.10和15.04上安装Unity 8。


到目前为止，开发者已经可以通过ISO（主要途径）获得该 Unity 8 预览来进行测试。不过 Canonical 也通过LXC容器发布了它。通过该方法，你可以使用 Unity 8 桌面进行会话，让它像其他桌面环境一样运行在Mir显示服务器上。就像你在 Ubuntu/Ubuntu Kylin 中安装Mate桌面，然后从LightDm登录屏幕选择桌面会话一样。

想试一试 Unity 8？让我们来看看如何安装它。

注：这是一个试验性预览，可能不是所有人都可以让它正确的工作。

### 在 Ubuntu/Ubuntu Kylin 中安装的 Unity 8 桌面

以下是安装和使用 Unity 8 的步骤：

#### 第1步（情况I）：在 Ubuntu 的12.04或14.04安装 Unity 8

如果您正在运行 Ubuntu 12.04 或 Ubuntu/Ubuntu Kylin 14.04，那么你必须使用官方PPA来安装Unity 8。使用以下命令进行安装：

sudo apt-add-repository ppa:unity8-desktop-session-team/unity8-preview-lxc

sudo apt-get update

sudo apt-get upgrade

sudo apt-get install unity8-lxc
#### 第1步（情况II）：在 Ubuntu 的14.10或15.04安装 Unity 8

如果您正在运行 Ubuntu/Ubuntu Kylin 14.10 或 15.04，那么Unity 8 LXC 已经在源中准备好了。你只需要运行下面的命令：
sudo apt-get update

sudo apt-get install unity8-lxc
#### 第2步：设置 Unity 8 桌面预览LXC
安装 Unity 8 LXC 后，使用以下的命令对其进行配置：
sudo unity8-lxc-setup
配置会耗费一些时间，所以要有一定的耐心。该命令会自动下载ISO，然后解压缩，接着完成一些必要的设置来使其工作。还将安装一个略微改动过的 LightDM。上述工作都完成之后，需要重新启动。
#### 第3步：选择 Unity 8
重新启动后，在登录界面，点击登录名旁边的 Ubuntu/Ubuntu Kylin 图标：

![](http://www.ubuntukylin.com/upload/images/unity82.jpg)
你应该可以在这里看到 Unity 8 的选项。选择它：

![](http://www.ubuntukylin.com/upload/images/unity83.jpg)

### 卸载 Unity 8 LXC
如果您发现 Unity 8 漏洞太多，或者你不喜欢它，你可以以相同的方式切换回默认的Unity版本。此外，您还可以使用以下命令删除 Unity 8：
sudo apt-get remove unity8-lxc
这将从 LightDM 屏幕移除 Unity 8 选项，但配置仍然保留着。

 

以上就是你在 Ubuntu/Ubuntu Kylin 中安装带有Mir的 Unity 8 的全部过程，试玩后请分享你关于 Unity 8 的想法哦！
