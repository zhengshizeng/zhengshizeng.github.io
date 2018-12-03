---
title: Win命令行下关闭某端口被占用程序
date: 2018-12-03 15:15:37
tags: [cmd]
categories: "cmd"
---

> Netstat是控制台命令,是一个监控TCP/IP网络的非常有用的工具。
<!-- more -->
###### 1.根据端口查询程序PID   

```
netstat -ano | findstr "7001"
```
命令行下 输入 netstat /? 可查看帮忙. 
参数 | 功能
---|-----
 -a | 显示所有连接和侦听端口
 -n | 以数字形式显示地址和端口号。
 -o | 显示拥有的与每个连接关联的进程 ID。
---   
> tasklist用来显示运行在本地或远程计算机上的所有进程
###### 2.根据PID查看是哪个进程或者程序占用了,如pid =5288

```
tasklist | findstr "5288"
```
---
> taskkill是用来终止进程的.
###### 3.杀死进程,根据上一指令查询出来的，如 node.exe

```
taskkill /f /t /im node.exe
```

