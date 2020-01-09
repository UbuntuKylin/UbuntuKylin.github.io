---
title: 如何解决 Ubuntu Kylin 下不能记住亮度设置的问题
toc: true
date: 2019-06-24 14:29:06
tags:
categories:
---


之前有接到用户反馈 Ubuntu Kylin 无法记住亮度设置的问题，每次开机或从睡眠状态下唤醒，亮度会恢复至最大值或最小值。这几天浏览itsfoss网站时，无意间发现了这个解决方法。

外国网友Norbert写了一个脚本，能让 Ubuntu Kylin 记住亮度设置，不论是开机还是唤醒之后。为了能让你使用这个脚本更简单方便，他把这个适用于 Ubuntu 12.04、14.04 和 14.10 的PPA挂在了网上，此PPA同样也适用于 Ubuntu Kylin。你需要做的就是输入以下命令：

 * sudo add-apt-repository ppa:nrbrtx/sysvinit-backlight
 * sudo apt-get update
 * sudo apt-get install sysvinit-backlight

安装好之后，重启你的系统。现在就来看看亮度设置有没有被保存下来吧。

希望这篇小贴士能帮助到你。如果你有任何问题，就来这儿[点击此处](https://launchpad.net/~nrbrtx/+archive/ubuntu/sysvinit-backlight/+packages)提bug吧！ 
