---
title: 'Linux中，你一定要掌握的网络基本命令! '
toc: true
date: 2019-06-24 09:10:27
tags:
categories:
---





## Linux中，你一定要掌握的网络基本命令!

不论你是一个有追求的 Linux 系统管理者，或是 Linux 狂热者，这些基础且重要的 Linux 网络命令你一定要了解！

在学习 Linux 的过程中，大家都会非常注意命令行的运用，想必也看过很多书来进行学习。在今天的文章中，我（注：作者为 Abhishek Prakash）给大家总结一下曾让我在计算机网络工程这门课上，帮助我拿到高分的网络命令集。欢迎大家拿出小抄赶紧记上，希望对你也有用哦。

**网络连通性**
Ping：发送一个 ICMP 回声请求消息给主机，一直持续到到你按下 Ctrl+C 。Ping 表示一个包通过 ICMP 从你的机器发送出去，然后在IP层得到回应。Ping 可以检测你与另一台主机是否连通。
Telnet host：在指定的端口与主机交互。telnet 端口默认是 23。其他比较常用的端口有回送端口7，用来发送邮件 SMTP 25，用户查询79。使用 Ctrl+] 退出 telnet。

**ARP**
ARP 是用来将 IP 地址转换为以太网地址的。Root 用户可以增加/删除 ARP 条目。其中 ARP 的条目都是缓存在内核中的，一般在20分钟后会自动删除。但 root 用户可以创建永久性的 ARP 条目。
arp -a：打印 ARP 表
arp -s[pub]：增加条目
arp -a -d：删除所有条目

**路由**
netstat -r：打印路由表。路由表存储在内核中，ip 通过它来将包发送到外网。
routed：执行动态路由选择的 BSD 守护进程。实现 RIP 路由协议。只能在 root 权限下使用。
gated：gated 是实现 RIP 的另一个路由守护进程。同时使用 OSPF/EGP/RIP 。只能在 root 权限下使用。
traceroute：可用来追踪IP数据包经过的路由信息。
netstat -rnf inet：可显示 IPv4 的路由表。
sysctl net.inet.ip.forwarding=1：使数据包继续传递（把一个主机变成路由）。
route：route 命令用来在路由表中设置静态路由。所有从 PC 到 IP/SubNet 的信息都要经过指定的网关 IP。这命令还可以用来设定默认路由。
route add|delete [-net|-host]：添加/删除静态路由（如：route add 192.168.20.0/24 192.168.30.4）。
route flush：删除所有路由。
route add -net 0.0.0.0 192.168.10.2：增加一个默认路由。

**重要文件**
/etc/hosts：IP地址及名字
/etc/networks：IP地址及网络名字
/etc/protocols：协议号及协议名字
/etc/services：tcp/udp服务名字对应的端口号

**工具以及网络性能分析**
ifconfig[up]：开启接口
ifconfig[down|delete]：停止接口
tcpdump -i -vvv：抓取和分析数据包的工具
netstat -w [seconds] -l [interface]：显示网络设置和数据

**其他**
nslookup：通过查询 DNS 服务器将 IP 转换成名字，或把名字转换成 IP。比如，nslookup ubuntukylin.com 会得到 ubuntukylin.com 的IP地址。
ftp：在本地主机和远程主机之间传送文件。
rlogin：远程登陆主机。
