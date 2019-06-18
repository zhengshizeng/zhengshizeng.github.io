---
title: ubuntu编译ffmpeg
date: 2018-11-28 06:19:02
tags: [ubuntu,ffmpeg,make]
categories: "Linux"
---
> ffmpeg 源码编译
<!-- more -->
## Ubuntu上编译安装
#### 1.安装yasm 不安装后面会报错：报错 yasm/nasm 包不存在或者很旧 
```
sudo apt-get install yasm 
```
#### 2.安装第三方库:x264
不安装H.264第三方库使用H.264的时候会报错Cannot load libcuda.so.1
[下载网址](http://download.videolan.org/pub/videolan/x264/snapshots/)
文件名: last_stable_x264.tar.bz2
```
./configure–enable−shared–disable−asm./configure–enable−shared–disable−asm make 
make install
```
### 安装ffmpeg
#### 1.解压缩
```
tar -xvjf ffmpeg-3.4.1.tar.bz2
```
#### 2.配置ffmpeg
```
./configure --enable-shared --enable-libx264 --enable-gpl --prefix=tmp
```
--enable-shared：指定生成动态库，默认是静态库。
#### 3.安装ffmpeg
```
make
make install 
```
###### 在tmp目录中可以看到bin include lib share

###### ffmpeg正常安装后执行ffmpeg时出现如下错误：    
==ffmpeg: error while loading shared libraries: libavdevice.so.53: cannot open shared object file: No such file or directory==

##### 解决办法：   
编辑 /etc/ld.so.conf 文件    
```
vi /etc/ld.so.conf
```
加入：lib 目录  然后执行
```
ldconfig
```

##### ESM6802 板子编译    
 
```
./configure --enable-cross-compile --arch="armv7-a"
--enable-pic      
--enable-shared 
--disable-static 
--target-os=linux 
--cross-prefix="arm-emtronix-linux-gnueabi-"    
--sysroot="/opt/fsl-imx-x11/4.1.15-2.0.1/sysroots/cortexa9hf-neon-emtronix-linux-gnueabi"
--disable-asm --extra-cflags="-march=armv7-a -mfpu=neon -mtune=cortex-a9-mfloat-abi=hard -mcpu=cortex-a9 -fPIC" 
--extra-ldflags="-march=armv7-a -mfpu=neon -mtune=cortex-a9-mfloat-abi=hard -mcpu=cortex-a9 -fPIC" 
--prefix=tmp
```

