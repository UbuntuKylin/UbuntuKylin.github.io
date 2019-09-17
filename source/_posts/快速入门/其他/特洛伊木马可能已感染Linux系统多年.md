---
title: 特洛伊木马可能已感染Linux系统多年
toc: true
date: 2019-06-24 14:31:08
tags:
categories:
---


<img src="http://www.ubuntukylin.com/upload/images/trojan-word-cloud(1).jpg"></img>  
关于为什么要转用Linux的论据之一就是Linux是安全的、无病毒的。“Linux对病毒免疫”这一观点被多数Linux用户广泛接受，然而这只在一定程度上成立，并非完全如此。
       与其它操作系统一样，Linux同样无法对恶意代码、木马、rootkit、病毒等完全免疫，已知存在几种著名的Linux病毒。但是如果和Windows相比，数量非常有限。既然如此又何必故话重提呢？这是因为一种新的木马已在市场上被探测到，有可能影响Linux系统。

**Turla同样可以感染Linux系统**
       数月前一款名为Turla的精巧间谍程序被探测到，该病毒被认为源自俄罗斯并且受到俄罗斯政府的支持。间谍程序以欧洲和美国的政府机构为目标已长达四年之久。在最近的报告中，Kaspersky的研究者发现Turla不仅感染Windows系统，同样感染Linux操作系统。Kaspersky研究者将其描述为“Turla迷题的丢失片段”（missing piece of Turla puzzle）。
**什么是Turla的Linux模块以及该模块有何危险性？**
       “Linux Turla模块是一个静态编译的C/C++模块，去除了符号信息目的是增加分析的难度。其功能包括隐藏的网络通信、任意地远程命令执行和远程管理。大部分代码来自公开来源”。
       报告还提到该木马在执行任意远程命令时不需要提权，无法被常用的管理工具发现。就个人而言，这种说法值得怀疑。因此，作为Linux桌面用户是否会感到担忧呢？在我们经历过ShellShock Linux bug之后，现在就崩溃还为时过早。Turla最初针对的是政府机构而不是普通用户。我们可以等待和观察更多、更详细的消息。
