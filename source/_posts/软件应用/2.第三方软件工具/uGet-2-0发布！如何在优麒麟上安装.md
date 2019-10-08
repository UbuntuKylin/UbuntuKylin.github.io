---
title: uGet 2.0发布！如何在优麒麟上安装
toc: true
date: 2019-06-24 14:29:27
tags:
categories:
---

![](https://www.ubuntukylin.com/upload/images/uget1.jpg)

※ 多连接

※ 多协议

※ 批量下载

※ 全局默认

※ 分类的默认值

※ 速度限制

在 uGet 2.0 上有什么新的东西呢？

uGet 2.0 是一个主要的版本，在外观、性能和新特性方面都带来一些新的变化。

**应用领域：**

 * 每个类别都有对应的数据文件。（文件格式是JSON）
 * 程序可以在全局限速模式为每次下载设置优先级。
 * 按文件扩展名、主机或方案自动分类。
 * 用户可以更改类别的顺序。
 * 所有的数据文件使用JSON格式。（不兼容uGet1）
 * 全局速度控制可以应用到所有的插件。
 * 忽略剪贴板和命令行现有的网址。

**curl 插件：**

 * 支持多线程下载。
 * 支持镜像。
 * 支持 aria2 控制文件格式 v1（aria2 V1.4.1）。
 * 在下载前根据文件大小预先分配空间。
 * 与 uGet1 不兼容，uGet 的下载文件无法在 uGet2 中恢复。

**aria2插件：**

 * 更好的 BitTorrent 和 Metalink 的支持。
 * 支持 JSON-RPC 批处理请求，以改善 aria2 远程下载。
 * 支持 aria2“-out”参数来设置输出文件名。
 * 支持RPC授权密钥令牌（Aria2 v1.8.4新增功能）
 * 新增“拆分”选项，如果用户指定了镜像，可以避免更少的连接。

**GTK +用户界面：**

 * 新的设置对话框。
 * 为触摸屏自动调整类别选择的主窗口。
 * 记住类别的选择和位置窗格。
 * 按照下载状态排序。
 * 下载完成后程序可以执行自定义的命令。
 * 删除功能：根据文件类型启动应用程序。
 * 发生错误时不显示完成，而是通知错误。
 * 可以在滑动窗显示 uGet RSS 消息。
 * 提供 uget-1to2（或uget-GTK-1to2）转换旧uGet文件。

**在优麒麟（Ubuntu Kylin）上安装uGet 2.0**

要在 Ubuntu Kylin 15.04，14.10 和 14.04 中安装 uGet 的最新稳定版本，请在终端中使用下面的命令：

 * sudo apt-add-repository ppa:plushuang-tw/uget-stable

 * sudo apt-get update

 * sudo apt-get install uget aria2

 

本教程图片来自于 uGet 官方网站，希望这个教程对你有所帮助。
