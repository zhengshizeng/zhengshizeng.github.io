---
title: ubuntu编译VLC(vlc-3.0.4)
date: 2018-11-30 06:09:01
tags: [ubuntu,VLC,make]
categories: "Linux"
---
> ubuntu编译VLC(vlc-3.0.4) 源码
> VLC多媒体播放器（最初命名为VideoLAN客户端）是VideoLAN计划的多媒体播放器。

<!-- more -->

##### 1.首先安装必须的依赖软件，打开终端，执行：
```
sudo apt-get install git libtool build-essential pkg-config autoconf
```
##### 2.从 http://www.videolan.org/vlc/download-sources.html 下载vlc-3.0.4源码，将其存放到/home/test/VLC目录下，解压缩：
```
xz -dk vlc-3.0.4.tar.xz 
tar xvf vlc-3.0.4.tar
cd vlc-3.0.4
```
##### 3. 获取第三方库：
```
sudo apt-get build-dep vlc
```
注意这个地方开始的时候老是提示无法获取依赖库，原因是所选择的服务器他不提供这个依赖库，所以需要选择最佳服务器，设置-》软件和更新-》下载自-》选择最佳服务器。

##### 4. 配置VLC，指定VLC的安装目录/home/test/VLC：
```
./configure --prefix=/home/test/VLC
```
直接 ./configure 也可以，有报错的时候 sudo apt-get build-dep vlc多下几次。
##### 5. 编译VLC：
```
make
```
##### 6. 运行VLC，验证是否一切正确：
```
./vlc
```
##### 7. 安装VLC(可选)：
```
make install
```


