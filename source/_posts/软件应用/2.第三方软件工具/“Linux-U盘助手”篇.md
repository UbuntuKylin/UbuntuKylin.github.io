---
title: '“Linux U盘助手”篇 '
toc: true
date: 2019-06-29 11:47:02
tags:
categories:
---

### 一、软件的下载及编译：

 1. 在CODE平台上访问项目https://code.csdn.net/silulusilulu/udmanager_linux/tree/master 。

 2. 复制ssh地址git[at]code[dot]csdn[dot]net:silulusilulu/udmanager_linux.git。

 3. 执行gitclone，将项目导入本地。

<img src="http://www.ubuntukylin.com/upload/images/1(2).png"></img>

 

 4. 在项目main/目录中执行qmake(qt4)，生成Makefile文件。（建议配置好qt环境变量，或找到qmake的相应路径）
<img src="http://www.ubuntukylin.com/upload/images/2(2).png"></img>

 5. 执行make命令，编译软件。

<img src="http://www.ubuntukylin.com/upload/images/3(1).png"></img>

### 二、软件的执行及功能演示：

 1. 进入bin/目录运行软件，以root权限运行后软件处于u盘拔插的监听状态。

![]()

 2. 插入u盘后，桌面上弹出悬浮窗口，可自由拖动。

![]()

 3. 双击悬浮窗口，提示用户选择挂载目录。建议选择空目录作为挂载点，否则会覆盖丢失目录中原有数据。

![]()

 4. 挂载目录选择完成后，进入主操作窗口（若挂载不成功会重复提示挂载）。

![]()

 5. 主窗口可对u盘进行信息检测或操作。窗口上部为u盘信息检测部分，点击按钮，可得到u盘的信。

![]()

 6. 点击Deepcheck I/O Speed按钮可深度测试u盘的读写速度，包括cache速度。

![]()

 7. 点击fsck按钮可对u盘的文件系统进行扫描修复。（u盘内数据越多，检测速度越慢）

![]()

 8. 点击formate按钮可对u盘进行格式化处理。格式化后原有数据丢失。软件提供几种常用的文件系统类型供用户选择，其中ext*文件系统格式化需要较长时间。若格式化过程中中断，则u盘文件系统损坏。
![]()

选择完成后点击ok按钮则对u盘进行格式化。

 9. 主窗口下部为软件执行过程的中间数据，可与结果一同供用户参考，也可点击detail按钮对细节进行隐藏或显示操作。

![]()

 10. 最小化主窗口则弹出悬浮窗口。

 11. 拔出u盘则隐藏主窗口和悬浮窗口。
 12. 软件运行后一直处于监听状态，可反复拔插u盘。

 13. start按钮可对u盘的监听线程进行开启或关闭，建议一直保持开启，否则可能会有未知错误。。。

 14. 目前软件不具有同时操作多个u盘的功能。
