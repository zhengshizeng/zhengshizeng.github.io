---
title: 解决Navicat连接MySQL总是报错1251的方法
date: 2018-12-03 15:20:02
tags: [MySQL,Navicat]
categories: "error"
---

> Navicat连接不上，总是报错1251;   
原因是MySQL8.0版本的加密方式和MySQL5.0的不一样，连接会报错.
<!-- more -->
1.先通过命令行进入mysql的root账户：
```
mysql -uroot -pz123456
```
2.更改加密方式：
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'z123456' PASSWORD EXPIRE NEVER;
```
3.更改密码：
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'z123456';
```
4.刷新：
```
FLUSH PRIVILEGES;
```