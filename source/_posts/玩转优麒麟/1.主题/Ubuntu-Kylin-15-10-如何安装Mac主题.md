---
title: Ubuntu Kylin 15.10 如何安装Mac主题
toc: true
date: 2019-06-24 14:27:38
tags:
categories:
---


### 下载最新的mac壁纸：
 * wget http://drive.noobslab.com/data/Mac-15.10/MacBuntu-Wallpapers.zip


### MacBuntu OSŸ主题，图标和光标：

 * sudo add-apt-repository ppa:noobslab/themes
 * sudo apt-get update
 * sudo apt-get install macbuntu-icons-v6
 * sudo apt-get install macbuntu-ithemes-v6

卸载macbuntu OSY主题，图标和光标。

 * cd /usr/share/icons/mac-cursors && sudo ./uninstall-mac-cursors.sh
 * sudo apt-get remove macbuntu-ithemes-v6 macbuntu-icons-v6


### Slingscold（替代的Launchpad）：

 * sudo add-apt-repository ppa:noobslab/apps

 * sudo apt-get update

 * sudo apt-get install slingscold


### 突变聚焦（替代苹果的Spotlight）：

 * sudo add-apt-repository ppa:noobslab/apps

 * sudo apt-get update

 * sudo apt-get install mutate


### Plank Dock（木板）：

 * sudo apt-get install plank

安装dock主题皮肤

 * sudo add-apt-repository ppa:noobslab/themes

 * sudo apt-get update

 * sudo apt-get install macbuntu-plank-theme-v6

卸载dock主题

 * sudo apt-get autoremove plank macbuntu-plank-theme-v6


### 应用MacBuntu开机画面/飞溅：

 * sudo add-apt-repository ppa:noobslab/themes

 * sudo apt-get update

 * sudo apt-get install macbuntu-bscreen-v6

如果不喜欢可以用下面命令卸载并回到ubuntu

 * sudo apt-get autoremove macbuntu-bscreen-v6


### 更换面板上的“Ubuntu桌面”字和“苹果”：

 * cd && wget -O Mac.po http://drive.noobslab.com/data/Mac-15.10/change-name-on-panel/mac.po

 * cd /usr/share/locale/zh_CN/LC_MESSAGES; sudo msgfmt -o unity.mo ~/Mac.po;rm ~/Mac.po;cd

不喜欢可以回到ubuntu用下面命令恢复

 * cd && wget -O Ubuntu.po http://drive.noobslab.com/data/Mac-15.10/change-name-on-panel/ubuntu.po

 * cd /usr/share/locale/zh_CN/LC_MESSAGES; sudo msgfmt -o unity.mo ~/Ubuntu.po;rm ~/Ubuntu.po;cd


### 苹果Logo：

 * wget -O launcher_bfb.png http://drive.noobslab.com/data/Mac-15.10/launcher-logo/apple/launcher_bfb.png

 * sudo mv launcher_bfb.png /usr/share/unity/icons/

恢复ubuntu ,logo

 * wget -O launcher_bfb.png http://drive.noobslab.com/data/Mac-15.10/launcher-logo/ubuntu/launcher_bfb.png

 * sudo mv launcher_bfb.png /usr/share/unity/icons/


### 安装工具来改变主题和图标：

 * sudo apt-get install unity-tweak-tool

 * sudo apt-get install gnome-tweak-tool


### 安装单色图标的LibreOffice：

 * sudo apt-get install libreoffice-style-sifr


### Mac字体：

 * wget -O mac-fonts.zip http://drive.noobslab.com/data/Mac-15.10/macfonts.zip

 * sudo unzip mac-fonts.zip -d /usr/share/fonts; rm mac-fonts.zip

 * sudo fc-cache -f -v


### 安装MacBuntu主题LightDM的Webkit迎宾：

 * sudo add-apt-repository ppa:noobslab/themes

 * sudo apt-get update

 * sudo apt-get install macbuntu-lightdm-v6

如果不能正常工作卸载可以恢复ubuntu迎宾

 * sudo apt-get remove macbuntu-lightdm-v6
![](https://www.ubuntukylin.com/ukylin/data/attachment/forum/201511/07/215036vvjjqn6mwmy6n4zv.jpg)
![](https://www.ubuntukylin.com/ukylin/data/attachment/forum/201511/07/215042g2ryutkts02ku2ka.png)

