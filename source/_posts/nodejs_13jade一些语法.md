---
title: 13jade一些语法
date: 2019-06-08 06:26:13
tags: [nodejs]
categories: "nodejs"
---
### 十三、jade一些语法
###### 1. 原样输出 加 |
```
html
  head
    script
      |window.onload=function (){
      | var oBtn=document.getElementById('btn1');
      | oBtn.onclick=function (){
      |   alert('aaaa');
      | };
      |};
  body
    |abc
    |ddd
    |213
```
###### 2. 原样输出 加 .  
表示下面的所有层级都原样输出  eg head.
```
html
  head.
    div
  body
    |abc
    |ddd
    |213
```
###### 3.include 加载外部文件
```
html
  head
    script
      include a.js
  body
    |abc
    |ddd
    |213
```
###### 4.#{name} 传参
```
html
  head
  body
    div 我的名字：#{a+b}
```
```
const jade=require('jade');

console.log(jade.renderFile('./views/7.jade', {pretty: true, a: 12, b: 5}));
```
###### 5.直接传 style json格式 class 数组格式
```
html
  head
  body
    div(style=json)
    div(class=arr)
    div(class=arr class="active")
    div(class=arr)
```
###### 6. 前面加 - 表示代码块
```
html
  head
  body
    -var a=12;
    -var b=5;
    div 结果是：#{a+b}
```
###### 7. for循环
```
html
  head
  body
    -for(var i=0;i<arr.length;i++)
      div=arr[i]
```
###### 8. 标签不转义 加! 号
```
  body
    div!=content
```
```
const jade=require('jade');

console.log(jade.renderFile('./views/12.jade', {pretty: true,
  content: "<h2>你好啊</h2><p>我是中国人</p>"
}));
```
###### 9. if 和 else
```
  body
    -var a=19;
    if(a%2==0)
      div(style={background:'red'}) 偶数
    else
      div(style={background:'green'}) 奇数
```
###### 10. case when  相当于 switch case
```
html
  head
  body
    -var a=1;
    case a
      when 0
        div aaa
      when 1
        div bbb
      default
        |不靠谱
```

###### 11. while 循环
```
  body
    -var a=0;
    while a<12
      if a%4==0 && a!=0
        div.last=a++
      else
        div=a++
```

#### 小示例
//index.jade
```

doctype
html
  head
    meta(charset="utf-8")
    title jade测试页面
    style.
      div {width:100px;height:100px;background:#CCC;text-align:center;line-height:100px;float:left;margin:10px auto}
      div.last {clear:left}
  body
    -var a=0;
    while a<12
      if a%4==0 && a!=0
        div.last=a++
      else
        div=a++
```
//index.js
```
const jade=require('jade');
const fs=require('fs');

var str=jade.renderFile('./views/index.jade', {pretty: true});

fs.writeFile('./build/index.html', str, function (err){
  if(err)
    console.log('编译失败');
  else
    console.log('成功');
});

```
