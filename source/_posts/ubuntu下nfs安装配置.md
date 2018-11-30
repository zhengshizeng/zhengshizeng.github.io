---
title: ubuntu下nfs安装配置
date: 2018-11-29 20:00:00
tags: [nfs,ubuntu,安装] 
categories: "Linux"
---


>NFS（Network File System）即网络文件系统，是FreeBSD支持的文件系统中的一种，它允许网络中的计算机之间通过TCP/IP网络共享资源。在NFS的应用中，本地NFS的客户端应用可以像访问本地文件一样透明地读写位于远端NFS服务器上的文件。
---
<!-- more -->

## NFS 服务端
#### 1.安装NFS
```
sudo apt-get install nfs-kernel-server 
```
#### 2. 建立nfs共享文件夹
```
sudo mkdir /home/test/nfs_dir
```
#### 3. 编辑/etc/exports配置nfs
```
sudo vim /etc/exports
```
#### 4.在文档的最后一行加入如下并保存退出
```
/home/test/nfs_dir *(rw,sync,no_root_squash,no_subtree_check)
```

/home/test/nfs_dir是要共享的目录    
*表示允许所有的网段访问，也可以使用具体的IP    
rw 读写访问sync 所有数据在请求时写入共享    
async nfs在写入数据前可以响应请求    
secure nfs通过1024以下的安全TCP/IP端口发送    
insecure nfs通过1024以上的端口发送    
wdelay 如果多个用户要写入nfs目录，则归组写入（默认）    
no_wdelay 如果多个用户要写入nfs目录，则立即写入，当使用async时，无需此设置。    
hide 在nfs共享目录中不共享其子目录    
no_hide 共享nfs目录的子目录    
subtree_check 如果共享/usr/bin之类的子目录时，强制nfs检查父目录的权限（默认）    
no_subtree_check 和上面相对，不检查父目录权限    
all_squash 共享文件的UID和GID映射匿名用户anonymous，适合公用目录。    
no_all_squash 保留共享文件的UID和GID（默认）    
root_squash root用户的所有请求映射成如anonymous用户一样的权限（默认）    
no_root_squas root用户具有根目录的完全管理访问权限    
anonuid=xxx 指定nfs服务器/etc/passwd文件中匿名用户的UID    

#### 5.重启rpcbind
```
sudo /etc/init.d/rpcbind restart 
```
#### 6.restart 重启nfs
```
sudo /etc/init.d/nfs-kernel-server 
```
#### 7.测试运行以下命令来显示一下共享出来的目录
```
showmount -e
```
---
##### 在目标机中挂载服务器的共享文件夹
> sudo mount -t nfs 192.168.2.109:/home/test/nfs_dir /mnt/nfs

把以上指令写到/etc/rc.local 当中可实现开机自动挂载   

---
### nfs client端安装与配置：

1. nfs client安装    
```
sudo apt-get install nfs-common
```
2. 查看nfs server上共享的目录    
```
showmount -e <ip address of nfs server>    
#例如showmount -e 192.168.xx.xx
```
3. 创建挂载点
```
mkdir /path-to-mount
chmod 777 -R /path-to-mount
mount -t nfs 192.168.xx.xx:/path-to-share /path-to-mount
```
4.开机自动挂载：
sudo mount -t nfs 192.168.2.109:/home/test/nfs_dir /mnt/nfs 添加到/etc/rc.local，开机就会自动挂载了


