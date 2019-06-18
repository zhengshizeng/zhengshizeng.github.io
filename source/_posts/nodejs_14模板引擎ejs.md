---
title: 14模板引擎ejs
date: 2019-06-08 06:26:14
tags: [nodejs]
categories: "nodejs"
---
### 十四、模板引擎ejs
```
npm install ejs
```
###### 1.变量 <%= name %>
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div>
      <%=json.arr[0].user%>
    </div>
  </body>
</html>
```
###### 2.for 循环
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <% for(var i=0;i<json.arr.length;i++){ %>
    <div>用户名：<%=json.arr[i].user%> 密码：<%=json.arr[i].pass%></div>
    <% } %>
  </body>
</html>
```
###### 3. - 表示原样输出不转义 =号转义
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <%
    var str="<div></div>";
    %>
    <%- str %>
    <%= str %>
  </body>
</html>
```
###### 4. include 
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <% if(type=='admin'){ %>
    <% include ../style/admin.css %>
    <%}else{%>
    <% include ../style/user.css %>
    <% } %>
  </body>
</html>
```
