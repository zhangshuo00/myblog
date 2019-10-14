---
title: nodeJs笔记（五）-net模块
date: 2019-10-14 20:39:55
tags:
---
## 服务器和客户端之间的交互
关于数据交互，可以想象成，server和client之间建立了一个pipe，pipe有两个分支，一个用于发送 s 到 c 的数据，一个用于发送 c 到 s 的数据。
`server会监听端口，而client去访问端口`，在Unix/Linux中，也可以监听文件。
## node如何开启一个 TCP 服务器
