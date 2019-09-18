---
title: 涨知识：如何在优麒麟和银河麒麟社区版上构建Linux跨平台的snap/flatpak包？
toc: true
date: 2019-06-24 09:04:32
tags:
categories:
---



**摘要**：Snap和Flatpak是新一代的Linux打包格式，它们通过将软件和依赖同时安装在一个沙盒中，使得采用snap和flatpak的应用，可以跨越不同的发行版，降低了开发和维护成本，同时大大提高了系统的安全性。本文将通过实例，来介绍如何在优麒麟/银河麒麟社区版上构建这两种跨平台的软件包。 
![](http://www.ubuntukylin.com/upload/201705/1494379156789730.jpg)
涨知识：如何在优麒麟和银河麒麟社区版上构建Linux跨平台的snap/flatpak包？

**首先，我们使用gtk编写一个最简单的“hello world”窗口程序。**

// 主程序main.c

＃include 
static gboolean quit(GtkWidget *widget, gpointer data)
{
　gtk_widget_destroy(widget);
　gtk_main_quit();
　return FALSE;

} 

int main(int argc, char *argv[])

{

　gtk_init(&argc, &argv); 

　GtkWidget *main_win;

　GtkWidget *label; 

　main_win = gtk_window_new(GTK_WINDOW_TOPLEVEL);

　gtk_window_set_title(GTK_WINDOW(main_win), "my window");

　gtk_window_set_default_size(GTK_WINDOW(main_win), 300, 100); 

　label = gtk_label_new("hello world!");

　gtk_container_add(GTK_CONTAINER(main_win), label); 

　g_signal_connect(G_OBJECT(main_win), "destroy", G_CALLBACK(quit), NULL); 

　gtk_widget_show_all(main_win);

　gtk_main(); 

　return 0;

} 

＃ CMake项目文件：CMakeLists.txt

project (hello)

cmake_minimum_required (VERSION 3.0.0) 

set (SRC_LIST main.c

) 

find_package (PkgConfig REQUIRED)

set (HELLO_DEPS

　gtk+-3.0

) 

pkg_check_modules (CACHED_HELLO_DEPS REQUIRED ${HELLO_DEPS})

include_directories (${CACHED_HELLO_DEPS_INCLUDE_DIRS})

link_directories (${CACHED_HELLO_DEPS_LIBRARY_DIRS})

add_executable (hello ${SRC_LIST})

target_link_libraries (hello ${CACHED_HELLO_DEPS_LIBRARIES})

install (TARGETS hello DESTINATION "bin") 

把这两个文件放在hello目录下，并将hello目录压缩成hello.tar.gz，放在主目录下供之后调用:

$ tar cvfz hello.tar.gz hello 

**其次，将其打包成snap格式。**

snaps 是Ubuntu推出的新一代打包格式，它安装迅速，创建方便，具有自动进行事务性更新的能力，可以在众多 Linux 桌面、服务器、云或者设备上完美、安全地运行。 

安装snapd(运行和管理snaps所需的服务)和snapcraft(构建snap包的工具)

$ sudo apt install snapd snapcraft

（其他系统安装方式请参见：[点击此处](https://snapcraft.io/docs/core/install)） 

初始化:

$ mkdir hello_snap && cd hello_snap

$ snapcraft init 

这会在你的目录下产生“snap/snapcraft.yaml”这个文件，而这个文件控制着snap包的构建过程以及向用户暴露的属性。(在16.04系统上，比如银河麒麟社区版和优麒麟16.04，直接在本目录下生成snapcraft.yaml文件，且默认内容也更简单) 

默认产生的snapcraft.yaml是这样的：

name: my-snap-name # you probably want to 'snapcraft register'

version: '0.1' # just for humans, typically '1.2+git' or '1.3.2'

summary: Single-line elevator pitch for your amazing snap # 79 char long summary

description: |

  This is my-snap's description. You have a paragraph or two to tell the

  most important story about your snap. Keep it under 100 words though,

  we live in tweetspace and your description wants to look good in the snap

  store.

grade: devel # must be 'stable' to release into candidate/stable channels

confinement: devmode # use 'strict' once you have the right plugs and slots 

其中：

grade: 定义此snap的质量等级，“devel”表示开发版本，“stable”表示稳定版本。

confinement: 定义此snap的限制级别，“strict”,“devmode”或“classic”，每个等级，软件具有的权限不同，具体区别见：[点击此处](https://snapcraft.io/docs/reference/confinement)

parts：snaps的主要构建部分，包括创建snap的源码，包，压缩包和组织步骤。

yaml文件完整语法规则在：[点击此处](https://snapcraft.io/docs/build-snaps/syntax)

根据本例，修改默认内容为如下：

name: hello-snap

version: '0.1'

summary: Say hello.

description: |

　Open a window, and say hello to the world!

grade: devel

confinement: devmode

apps:

　hello:

　command: desktop-launch hello

　plugs: 【x11】　　　　   ＃所需系统权限 

parts:

　gnu-hello:

　# 参见 'snapcraft plugins'

　source: /home/feng/snappy_flatpak/hello.tar.gz

　plugin: cmake

　stage-packages:

　- libmirclient9

after: 【desktop-gtk3】　　＃提供了各种gtk库 

对于银河麒麟社区版或者优麒麟16.04，由于snap版本更早，我们修改snapcraft.yaml为： 

//snapcraft.yaml

name: hello-snap

version: '0.1'

summary: Say hello.

description: |

　Open a window, and say hello to the world!

apps:

　hello:

　command: hello

　plugs: 【x11】

parts:

　gnu-hello:

　# 参见 'snapcraft plugins'

　source: /home/feng/snappy_flatpak/hello.tar.gz

plugin: cmake

stage-packages:

　- libcanberra-gtk-module:amd64

　- libcanberra-gtk3-module:amd64

after: 【desktop/gtk3】     　 #注意此处格式不一样 

编译：

$ snapcraft

此命令将会在本目录下（hello-snap）生成hello-snap_0.1_amd64.snap文件。(对于银河麒麟社区版，需要先把/etc/lsb-release中“DISTRIB_RELEASE=4.0.2”改为“ DISTRIB_RELEASE=16.04”) 

安装运行：

$ sudo snap install hello-snap_0.1_amd64.snap --devmode  // 以开发者模式安装

$ hello-snap.hello       // 最终的程序名构成为“name”.“apps”

对于银河麒麟社区版和优麒麟16.04,通过以下命令打开：

$ /snap/bin/hello-snap.hello 

你可以将此snap包上传至ubuntu 商店(可以通过snap find 查看ubuntu 商店中现有的软件)，或者直接发送到其他操作系统上，然后通过sudo snap install 安装(需要先安装snapd)，非常方便。 

**然后，将其打包成flatpak格式。**

Flatpak是一种用于构建，分发，安装和运行应用程序的技术。它主要针对的是Linux桌面，通过在沙箱中隔离应用程序来提高Linux桌面的安全性，允许应用程序安装在任何Linux发行版上。 

我们先来了解几个基本概念：

 * 运行时(runtimes)

“运行时”提供应用程序所需的基本依赖。有各种各样的“运行时”,比如“ Freedesktop 运行时”，“ GNOME 运行时 ”。“ Freedesktop 运行时”包含一系列必要的库和服务，包括 D-Bus, GLib, PulseAudio, X11 和 Wayland 等。“ GNOME 运行时”基于“ FreeDesktop 运行时”，增加了一些GNOME平台相关的库，比如GStreamer, GTK+, GVFS等。必须针对运行时构建每个应用程序，并且必须在主机系统上安装此运行时才能运行应用程序。用户可以同时安装多个不同的运行时，包括不同版本的同一个运行时。 

 * SDK（软件开发套件）

SDK也是一个“运行时”，是用于构建应用程序的特殊类型的运行时，它包含了构建和打包工具，如头文件，编译器和调试器。通常，SDK与“运行时”配对，由应用程序使用。 

 * 沙箱

使用Flatpak，每个应用程序都是在孤立的环境中构建和运行的。默认情况下，应用程序只能“查看”自身及其“运行时”,访问用户文件，网络，graphics sockets，总线和设备上的子系统必须明确授予权限，访问其他内容（如其他进程）是不允许的。 

 * 安装Flatpak

对于优麒麟16.04，银河麒麟社区版:

$ sudo apt install software-properties-common elfutils

$ sudo vim /etc/apt/sources.list.d/alexlarsson.list

//往alexlarsson.list添加如下两行:

deb http://ppa.launchpad.net/alexlarsson/flatpak/ubuntu xenial main

deb-src http://ppa.launchpad.net/alexlarsson/flatpak/ubuntu xenial main

$ sudo apt update

$ sudo apt install flatpak　flatpak-builder  

对于优麒麟17.04：

$ sudo apt install flatpak　flatpak-builder 

安装程序所需的“运行时”和Sdk：

$ flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo

$ flatpak install gnome org.gnome.Platform//3.24 org.gnome.Sdk//3.24 

初始配置：

$ mkdir hello-flatpak && cd hello-flatpak

$ gedit com.kylin.Hello.json

添加以下内容至com.kylin.Hello.json文件：

{

　"app-id": "com.kylin.Hello",

　"runtime": "org.gnome.Platform",　　＃所需“运行时”

　"runtime-version": "3.24",　　　　　

　"sdk": "org.gnome.Sdk",　　　　　　 ＃所需Sdk

　"command": "hello",

　"finish-args": 【"--socket=x11"】,　　＃所需系统权限

　"modules": [

　{

　"name": "hello",

　"cmake": true,

　"sources":[

　 {

　"type": "archive",

　"path": "/home/feng/snappy_flatpak/hello.tar.gz"

　}

　]

　}

　]

}

json文件等同于前文snap的yaml文件，包含着构建flatpak包的所有信息。 

编译、安装、运行：

$ flatpak-builder --repo=repo hello com.kylin.Hello.json

$ flatpak --user remote-add --no-gpg-verify --if-not-exists tutorial-repo repo

$ flatpak --user install tutorial-repo com.kylin.Hello

$ flatpak run com.kylin.Hello 

你可以将程序打包成flatpak格式，分发出去：

$ flatpak build-bundle repo hello.flatpak com.kylin.Hello 

然后在另一个系统安装这个程序（需要先安装相应“运行时”和Sdk）：

$ flatpak install --user --bundle hello.flatpak 

或者托管在仓库里（官方推荐方式），具体见：http://docs.flatpak.org/en/latest/distributing-applications.html

更多详细信息，可以点击以下链接：

snap:[点击此处](https://www.ubuntu.com/desktop/snappy)    

flatpak:[点击此处](http://flatpak.org/)
