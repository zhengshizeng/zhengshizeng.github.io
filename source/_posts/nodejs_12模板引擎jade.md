---
title: 12模板引擎jade
date: 2019-06-08 06:26:12
tags: [nodejs]
categories: "nodejs"
---
### 十二、模板引擎jade
```
npm install jade
npm install ejs
```
###### jade-破坏式、侵入式、强依赖
1.  根据缩进，规定层级
2.  属性放在()里面，逗号分隔
3.  内容空个格，直接往后堆
```
html				<html>
	head				<head>
		style				<style></style>
					</head>
	body				<body>
		div				<div></div>
		div				<div></div>
					</body>
				</html>
```
**属性**
```
script(src="a.js") //jade写法
<script src="a.js"></script>
```
**内容**
```
a(href="http://www.zhinengshe.com/") 官网
<a href="http://www.zhinengshe.com/">官网</a>
```
##### style="width:200px;height:200px;background:red;"
1. 普通属性写法
```
    div(style="width:200px;height:200px;background:red")
```
2. 用json
```
div(style= {width: '200px', height: '200px', background: 'red'})
```
##### class="aaa left-swrap active"
1. 普通属性写法
```
    div(class="aaa left-warp active")
```
2. 用arr
```
div(class= ['aaa', 'left-warp', 'active'])
```

###### a. jade.render('字符串');   
```
const jade=require('jade');
var str=jade.render('html');
console.log(str);
```
###### b. jade.renderFile('模板文件名', 参数)   
```
const jade=require('jade');
var str=jade.renderFile('./views/8.jade', {pretty: true});
//var str=jade.renderFile('./views/8.jade');//pretty 排版美化
console.log(str);
```

---

###### ejs-温和、非侵入式、弱依赖
<%= name %>
```
const ejs=require('ejs');

ejs.renderFile('./views/1.ejs', {name: 'blue'}, function (err, data){
  if(err)
    console.log('编译失败');
  else
    console.log(data);
});

```
```
//1.ejs
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    我的名字叫：<%= name %>
  </body>
</html>

```
