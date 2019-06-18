---
title: 02nodeJS--简单http服务器
date: 2019-06-08 06:25:02
tags: [nodejs]
categories: "nodejs"
---

##### 二、nodeJS—— 简单http服务器   
server.js
```
const http=require('http'); //加载http 模块
//request	请求	输入-请求的信息
//response	响应	输出-输出的东西  
var server=http.createServer(function (req, res){
  switch(req.url){
    case '/1.html':
      res.write("111111");
      break;
    case '/2.html':
      res.write("2222");
      break;
    default:
      res.write('404');
      break;
  }
  res.end();
});
//监听
server.listen(8080);

//http://localhost:8080/
```
