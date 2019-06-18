---
title: 10express了解、中间件、链式操作
date: 2019-06-08 06:26:10
tags: [nodejs]
categories: "nodejs"
---
### 十、express 了解
#### Express：
##### 1. 数据：GET、POST
###### GET-无需中间件
req.query
```
server.use('/', function (req, res){
  console.log(req.query); //GET
});
```
###### POST-需要"body-parser"
```
const express=require('express');
const bodyParser=require('body-parser');

var server=express();
server.listen(8080);
//中间件body-parser 加工post数据然后放到 req.body里
//server.use(bodyParser.urlencoded({}));//不带参数
server.use(bodyParser.urlencoded({
  extended: false,                 //扩展模式
  limit:    2*1024*1024           //限制-2M
}));

server.use('/', function (req, res){
  console.log(req.body); //POST
});
```
##### 2. 中间件：使用、写、链式操作
###### 链式操作：
```
  server.use(function (req, res, next){});
  server.get('/', function (req, res, next){});
  server.post(function (req, res, next){});

  // next——下一个步骤
  next();

  server.use('/login', function (){
    mysql.query(function (){
      if(有错)
        res.emit('error');
      else
        next();
    });
  });
```
###### 中间件(body-parser)、自己写中间件
body-parser
```
  server.use(bodyParser.urlencoded({}));//不带参数
  server.use('/', function (req, res){
    console.log(req.body); //POST
});
 ```

自己写的中间件my-body-parser.js
```
const querystring=require('querystring');

module.exports=function (req, res, next){
      var str='';
      req.on('data', function (data){
        str+=data;
      });
      req.on('end', function (){
        req.body=querystring.parse(str);

        next();
      });
}
```
使用
```
const bodyParser2=require('./libs/my-body-parser');
server.use(bodyParser2);
```


















