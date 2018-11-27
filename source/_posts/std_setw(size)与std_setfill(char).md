---
title: std_setw(size)与std_setfill(char)
date: 2018-11-03 09:36:54
tags: [C++, MFC]
categories: "C++"
---

> std::setw(size)与 std::setfill(char)
#### 功能:
std::setw ：需要填充多少个字符,默认填充的字符为' '空格   
std::setfill：设置 std::setw 将填充什么样的字符,如:std::setfill('\*')   

<!-- more -->


头文件:
#include <iostream>
#include <iomanip>
using namespace std;



```
#include <tchar.h>
#include <iostream>
#include <iomanip>

int _tmain(int argc, _TCHAR* argv[])
{
     int a = 1;
     //输出:    1 前面三个空格填充
     std::cout<<std::setw(4)<<a<<std::endl;
     //输出: ***1 设置用*号填充
     std::cout<<std::setw(4)<<std::setfill('*')<<a<<std::endl;

     //输出:***12
     int b = 2;
     std::cout<<std::setw(4)<<std::setfill('*')<<a<<b<<std::endl;
     system("pause");
     return 0;
}
```

