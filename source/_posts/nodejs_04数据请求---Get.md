---
title: 04数据请求 ---Get
date: 2019-06-08 06:26:04
tags: [nodejs]
categories: "nodejs"
---
##### 四、数据请求 ---Get
前台->form、ajax、jsonp 等   
后台->一样  都是 http请求   
**请求方式**：   
1.GET		数据在url中   
2.POST		数据不在url中   
......
---
from.html
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <form action="http://localhost:8080/aaa" method="get">
      用户：<input type="text" name="user" value=""><br>
      密码：<input type="password" name="pass" value=""><br>
      <input type="submit" value="提交">
    </form>
  </body>
</html>
```
###### GET数据解析
1.自己切   
```
const http=require('http');
http.createServer(function (req, res){
  var GET={};
  if(req.url.indexOf('?')!=-1){
    var arr=req.url.split('?');
    //arr[0]=>地址  '/aaa'
    var url=arr[0];
    //arr[1]=>数据  'user=blue&pass=123456'

    var arr2=arr[1].split('&');
    //arr2=>['user=blue', 'pass=123456']

    for(var i=0;i<arr2.length;i++){
      var arr3=arr2[i].split('=');
      //arr3[0]=>名字   'user'
      //arr3[1]=>数据   'blue'
      GET[arr3[0]]=arr3[1];
    }
  }else{
    var url=req.url;
  }
  console.log(url, GET);
  //req获取前台请求数据
  res.write('aaa');
  res.end();
}).listen(8080);
```
2.querystring 
```
const http=require('http');
const querystring=require('querystring');

http.createServer(function (req, res){
  var GET={};
  if(req.url.indexOf('?')!=-1){
    var arr=req.url.split('?');
    var url=arr[0];
    
    GET=querystring.parse(arr[1]);
  }else{
    var url=req.url;
  }
  console.log(url, GET);
  //req获取前台请求数据
  res.write('aaa');
  res.end();
}).listen(8080);
```
3.urlLib   
```
const http=require('http');
const urlLib=require('url');

http.createServer(function (req, res){
  var obj=urlLib.parse(req.url, true);

  var url=obj.pathname;
  var GET=obj.query;

  console.log(url, GET);

  //req获取前台请求数据
  res.write('aaa');
  res.end();
}).listen(8080);
```
