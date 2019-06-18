---
title: 05数据请求---post
date: 2019-06-08 06:26:05
tags: [nodejs]
categories: "nodejs"
---
##### 五、数据请求 ---post
###### 1.POST数据接收：POST数据比GET大得多
POST很大——分段   
data	一段数据   
end	全部到达
```
const http=require('http');
const querystring=require('querystring');

http.createServer(function (req, res){
  //POST——req
  var str='';   //接收数据
  //data——有一段数据到达(很多次)
  var i=0;
  req.on('data', function (data){
    console.log(`第${i++}次收到数据`);
    str+=data;
  });
  //end——数据全部到达(一次)
  req.on('end', function (){
    var POST=querystring.parse(str);
    console.log(POST);
  });
}).listen(8080);
```
###### 2.Get和Post综合、文件请求
```
const http=require('http');
const fs=require('fs');
const querystring=require('querystring');
const urlLib=require('url');

var server=http.createServer(function (req, res){
  //GET
  var obj=urlLib.parse(req.url, true);

  var url=obj.pathname;
  const GET=obj.query;

  //POST
  var str='';
  req.on('data', function (data){
    str+=data;
  });
  req.on('end', function (){
    const POST=querystring.parse(str);
    /*
    url——要什么
    GET——get数据
    POST——post数据
    */
    //文件请求
    var file_name='./www'+url;
    fs.readFile(file_name, function (err, data){
      if(err){
        res.write('404');
      }else{
        res.write(data);
      }
      res.end();
    });
  });
});

server.listen(8081);

```