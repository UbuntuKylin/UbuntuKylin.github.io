---
title: 如何修复Ubuntu Kylin 14.04丢失系统设置问题
toc: true
date: 2019-06-29 11:53:18
tags:
categories:
---
  最近有不少童鞋在安装搜狗输入法之后，决定卸载ibus输入法，结果导致系统设置变成如下这个“惨淡”景象，其它小伙伴都到哪里去了？  
<img src="https://www.ubuntukylin.com/upload/images/setting.png"></img> 
解决方法是：打开终端，然后执行以下命令 ——  
  sudo apt-get install ubuntu-desktop  
这相当于重新安装了Unity，该方法同样能够解决没有Unity启动器和指示面板的情形。
