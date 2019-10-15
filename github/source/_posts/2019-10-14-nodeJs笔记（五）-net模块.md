---
title: nodeJs笔记（五）-net模块
date: 2019-10-14 20:39:55
tags:
---
## 服务器和客户端之间的交互
关于数据交互，可以想象成，server和client之间建立了一个pipe，pipe有两个分支，一个用于发送 s 到 c 的数据，一个用于发送 c 到 s 的数据。
`server会监听端口，而client去访问端口`，在Unix/Linux中，也可以监听文件。
## node如何开启一个 TCP 服务器
>TCP全名为传输控制协议，在OSI模型中属于传输层协议
### 创建TCP服务器端
```js
var net = require('net');

var server = net.createServer(function(socket){
    socket.on('data',function(data){
        socket.write('hello');
    });

    socket.on('end',function(){
        console.log('connected filed');
    });

});
server.listen(8080,function(){
        console.log('server bound');
});
```
使用`telnet 192.168.91.144 8080`作为客户端对刚才创建的简单服务器进行会话交流
### TCP服务的事件
1. 服务器事件
   * listening：通过server.listen(port,listeningListener)，第二个参数传入
   * connection：通过net.createServer()，最后一个参数传递
   * close
   * error
2. 连接事件
   * data
   * end
   * connect
   * drain
   * error
   * close
   * timeout

## 构建UDP服务
>在UDP中，一个套接字可以与多个UDP服务通信，特点：面向事务提供简单的不可靠信息传输服务，但无须连接，资源消耗低，处理快速灵活。
### 创建UDP服务器端
```js
//创建UDP套接字
const dgram = require('dgram');

var socket = dgram.createSocket('udp4');
socket.bind(8080);//绑定端口

socket.on('message',(msg)=>{
    var line = msg.toString('utf-8');
    process.stdout.write(line,line.length);
});

socket.on('listening',()=>{
    console.log('server ready: ',socket.address());
});
```
### 创建UDP客户端
调用send()方法发送消息到网络中，`socket.send(buf, offset, length, port, address, [callback])`
```js
const dgram = require('dgram'),
    socket = dgram.createSocket('udp4');
var host = process.argv[2];
var port = process.argv[3];

process.stdin.on('data',(data)=>{
    var line = data.toString('utf-8');
    socket.send(line,0,line.length,port,host);
});
```
### UDP套接字事件
* message：接收到消息时触发该事件
* listening：当UDP套接字开始侦听时触发该事件
* close
* error






