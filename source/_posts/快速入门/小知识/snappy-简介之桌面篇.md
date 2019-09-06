---
title: snappy 简介之桌面篇
toc: true
date: 2019-06-24 14:25:38
tags:
categories:
---





## snappy 简介之桌面篇

Ubuntu/Ubuntu Kylin 1604 长期支持版引入了一种全新的打包方式——snappy, 这项技术极大的简化了开发者对应用程序的打包与分发的工作，克服了传统仓库的局限性，使得定期推送软件更新更加快捷方便，同时极大的提升了系统的安全性。 未来Ubuntu所有的系统都将使用Snappy，包括Ubuntu Desktop（桌面）, Ubuntu Phone（手机）, Ubuntu Core（物联网及云）等，我们开发的应用可以在多个不同平台尺寸的设备及云上运行而不必为某个设备单独开发．不仅如此，snap也移植到了其他 Linux发行版，比如Debian, Arch, Fedora, Gentoo等，你只需要把应用程序打包成snap,就可以在不同的发行版上安装它。

目前要在桌面上体验它，需要先安装snpad包：
 * sudo apt install snapd
  
之后，你就可以安装运行在商城中的应用：　　
 * sudo snap install ubuntu-calculator-app　　
 * ubuntu-calculatro-app.calculator　
　

当然，你也可以在dash中输入“Calculator"找到计算器（扁平图标的那个），然后打开它。这样你就在桌面上成功运行了手机版的计算器。

![](http://www.ubuntukylin.com/upload/201606/1466755449408310.jpg)

snap是管理系统上的snaps包的核心命令，　
 * snap --help      # 或者使用 'snap--help' 来寻求帮助
 * snap list       　# 列出已安装的snaps包
 * snap find    　　  # 列出所有可安装的snaps包
 * sudo snap install ubuntu-calculator-app.ubuntucoredev     #安装ubuntu 商店中的应用程序
 * sudo snap install xxx.snap     #安装本地snap包
 * sudo snap remove ubuntu-calculator-app     #卸载

更深入进去，snappy在桌面是如何工作的呢？
桌面版和服务器版的Snappy Ubuntu Core是如下的工作流程：
* Snaps包安装在主机文件系统的如下目录：
  /snap/$name/$version/
* 当一个snap应用启动时,会在系统中创建一个私有空间：
  × 创建一个slave mount namespace。
  × 创建一个私有的/tmp目录。
  × ubuntu-core-launcher 绑定挂载ubuntu-core 的/bin,/lib,/lib64,/sbin,/usr目录至应用程序空间。
  × ubuntu-core-launcher应用AppArmor/Seccomp 限制。
  × 应用程序启动：它可以看到主机的/dev, /proc/, /sys, /media 以及其他挂载点，但是会受到AppArmor的限制。

Snaps是受限的

在snaps下，应用程序运行在一个受限的沙箱中，与其他的应用程序是相互独立的。默认的限制规则允许同一个snap内的apps协同工作，但是无法访问其他apps，用户会话或者系统都是受限的。实现这个沙箱机制的技术涉及AppArmor,seccomp,设备cgroups,每个应用一个私有的 /tmp目录，per-app devpts 以及传统Unix权限机制。snappy 通过snap包内YAML文件配置具体受限规则。

更详细的信息，请浏览https://developer.ubuntu.com/en/desktop/
