---
title: 08自定义模块
date: 2019-06-08 06:26:08
tags: [nodejs]
categories: "nodejs"
---
##### 八.自定义模块
```
graph LR
A(模块化)-->B(系统模块)
A-->C(自定义模块)
```
---
### 1. 模块组成
```
require     //引入其他模块
exports     //一个一个输出
module      //批量输出
```
### 2. npm
##### npm：NodeJS Package Manager(NodeJS包管理器)
1. 统一下载途径 node_modules
2. 自动下载依赖

### 3. 发布自己的模块
```
npm init        //初始化
npm publish     //发布包
npm --force unpublish //卸载包
```
### [npm官网](https://www.npmjs.com/) 

1. 自己的模块
```
	require
	module
	exports
```
2. ```require``` 引入模块加	./	   
  
    1.如果有"./"   
    	从当前目录找   

    2.如果没有"./"   
    	先从系统模块   
	    再从node_modules找   


3. ".js"可选   
eg:  ```const mod1=require('./mod');```   

```
npm install xxx
npm uninstall xxx
```
**小结**   
---
1. 模块里面   
1.1 require——引入   
1.2 exports——输出   
1.3 module.exports——批量输出

2. npm   
2.1 帮咱们下载模块   
2.2 自动解决依赖   

3. node_modules	模块放这里


