---
title: 09express框架
date: 2019-06-08 06:26:09
tags: [nodejs]
categories: "nodejs"
---
### 1.安装
```
npm install express
```
### 2.配置
### 3.接收请求
### 4.响应 
---

express保留了原生的功能，添加了一些方法(send)，增强原有的功能

###### 三个步骤
1. 创建服务   
```
var server=express();
```
2. 监听  
```
server.listen(8080);
```
3. 处理请求
```
server.use('地址', function (req, res){
});
```
---
###### 三种方法：
```
.get('/', function (req, res){});
.post('/', function (req, res){});
.use('/', function (req, res){});
```
use 通吃，get和post都响应   

```
const express=require('express');
var server=express();
/*
server.get('/', function (){
  console.log('有GET');
});
server.post('/', function (){
  console.log('有POST');
});
*/
server.use('/', function (){
  console.log('use了');
});

server.listen(8080);

```
##### 小结

express框架：
1. 依赖中间件
2. 接收请求
  get/post/use
  get('/地址', function (req, res){});
3. 非破坏式的，原生的还可用，增加了一些方法。
  req.url
4. static用法
  const static=require('express-static');
  server.use(static('./www'));


```
const express=require('express');
const expressStatic=require('express-static');

var server=express();
server.listen(8080);

//用户数据
var users={
  'blue': '123456',
  'zhangsan': '654321',
  'lisi': '987987'
};

server.get('/login', function (req, res){
  var user=req.query['user'];
  var pass=req.query['pass'];

  if(users[user]==null){
    res.send({ok: false, msg: '此用户不存在'});
  }else{
    if(users[user]!=pass){
      res.send({ok: false, msg: '密码错了'});
    }else{
      res.send({ok: true, msg: '成功'});
    }
  }
});

server.use(expressStatic('./www'));
```

