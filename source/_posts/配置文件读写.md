---
title: 配置文件读写
date: 2016-01-01 09:36:54
tags: [C++,MFC] 
categories: "MFC"
---
> 在我们写的程序当中,总有一些配置信息需要保存下来,以便完成程序的功能,最简单的办法就是将这些信息写入INI文件中,程序初始化时再读入.
<!-- more -->
**配置文件中返回整形**  
[config]   
Num=2  
1.中括号内文字  
2.等号左边字符 
3.默认值没有找到配置的情况下  
4.配置文件名
```
uKch=GetPrivateProfileInt("CONFIG","Num",0,".\\config.ini");
```
**配置文件获取String**  
[config]  
str=中国人  
1.中括号内文字  
2.等号左边字符 
3.默认值  
4.返回的字符串  
```

GetPrivateProfileString("config","str","1",temp.GetBuffer(MAX_PATH),MAX_PATH,".\\config.ini");
```
**写配置文件**  
[config]  
str=中国人  

1.中括号内文字  
2.等号左边字符  
3.写入的字符  
```
::WritePrivateProfileString("config","str","中国人",".\\config.ini");
```

