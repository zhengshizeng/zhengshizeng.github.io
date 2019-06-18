---
title: 03文件操作fs---File System
date: 2019-06-08 06:26:03
tags: [nodejs]
categories: "nodejs"
---
##### 三、文件操作 fs——File System
###### readFile(文件名, function (err, data){}) 

```
const fs=require('fs');

//readFile(文件名, 回调函数)
fs.readFile('aaa.txt', function (err, data){
  if(err){
    console.log('读取失败');
  }else{
    console.log(data.toString());
  }
});
```
###### writeFile(文件名, 内容, function (err){})
```
const fs=require('fs');

//writeFile(文件名, 内容, 回调)
fs.writeFile("bbb.txt", "sdafasdwere", function (err){
  console.log(err);
});
```
###### http+fs 简单http服务
```
const http=require('http');
const fs=require('fs');

var server=http.createServer(function (req, res){
  //req.url=>'/index.html'
  //读取=>'./www/index.html'
  //  './www'+req.url
  var file_name='./www'+req.url;

  fs.readFile(file_name, function (err, data){
    if(err){
      res.write('404');
    }else{
      res.write(data);
    }
    res.end();
  });
});

server.listen(8080);
```
