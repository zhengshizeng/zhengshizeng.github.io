---
title: 11cookie和session
date: 2019-06-08 06:26:11
tags: [nodejs]
categories: "nodejs"
---
### 十一、cookie和session
http-无状态的,要保存用户数据所以就有了cookie和session
1. cookie：在浏览器保存一些数据，每次请求都会带过来
  *不安全、有限(4K)

2. session：保存数据，保存在服务端
  *安全、无限

--- 
session：基于cookie实现的   
  *cookie中会有一个session的ID，服务器利用sessionid找到session文件、读取、写入

  隐患：session劫持   
  
---
#### cookie
> 1. cookie空间非常小---省着用,精打细算
> 2. 安全性非常差,校验cookie是否被篡改过

##### a.发送cookie
```
res.secret='字符串';//加签名   这个可不写 server.use(cookieParser('签名字符串'));时已经加了
res.cookie(名字, 值, {path: '/', maxAge: 毫秒, signed: true});
//signed 是否加签名
//maxAge 有效期以毫秒为单位
//eg 
res.cookie('user', 'blue', {path: '/aaa', maxAge: 30*24*3600*1000});
```
##### b.读取cookie
cookie-parser
```
const cookieParser=require('cookie-parser');//加载
server.use(cookieParser());//使用

server.use('/', function (req, res){
  console.log(req.cookies);//cookies
  res.send('ok');
});
```
```
server.use(cookieParser('签名字符串'));
//发送时 signed: true有签名
server.use(function (){
  console.log('签名cookie：', req.signedCookies)
  console.log('无签名cookie：', req.cookies);
});
```
##### c.删除cookie
```
res.clearCookie(名字);
```
---

####   session
cookie-session
```
const cookieSession=require('cookie-session');//加载
/* 
    server.use(cookieSession({
	keys: [.., .., .., ..]
}));
*/
server.use(cookieParser());
server.use(cookieSession({
  name: 'sess',
  keys: ['aaa', 'bbb', 'ccc'],
  maxAge: 2*3600*1000
}));

server.use('/', function (req, res){
  if(req.session['count']==null){
    req.session['count']=1;
  }else{
    req.session['count']++;
  }

  console.log(req.session['count']);

  res.send('ok');
});

```
##### 删除session
```
delete req.session

	res.session['xxx']
	delete res.session['xxx'];
```
