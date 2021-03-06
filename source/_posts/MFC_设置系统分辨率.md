---
title: MFC_设置系统分辨率
date: 2018-11-03 09:36:51
tags: [C++, MFC]
categories: "MFC"
---

>在一些应用实例中，我们需要全屏显示程序，自适应的去调整控件的大小和位置有时候不太美观。
一个简单的方法，设置系统分辨率来完成全屏的显示。   
---

> 1.程序开启自动设置Window系统分辨率,使程序全屏显示
> 2.程序退出时还原 Window系统分辨率

<!-- more -->

.h 定义

```
	int SM_CXSCREEN_x, SM_CYSCREEN_y;
	void SetDevMode();
	void SetDevModeexit();
```

.cpp 实现

```
void CXXXXApp::SetDevMode()
{
	//保存原始分辨率退出后还原
	SM_CXSCREEN_x=GetSystemMetrics(SM_CXSCREEN);
	SM_CYSCREEN_y=GetSystemMetrics(SM_CYSCREEN);
	//要从配置文件读取 800X600
	if ( SM_CYSCREEN_y !=600 || SM_CXSCREEN_x !=800)
	{
		DEVMODE DevModez;
		EnumDisplaySettings(NULL,ENUM_CURRENT_SETTINGS,&DevModez);//获取当前的数据
		DevModez.dmPelsWidth =800;
		DevModez.dmPelsHeight=600;
		ChangeDisplaySettings(&DevModez,CDS_UPDATEREGISTRY);//设置生效
	}
}
void CXXXXApp::SetDevModeexit()
{
	int tempx,tempy;
 	tempx=GetSystemMetrics(SM_CXSCREEN);
 	tempy=GetSystemMetrics(SM_CYSCREEN);
 	if ( SM_CYSCREEN_y !=tempy || SM_CXSCREEN_x !=tempx)
 	{
 		DEVMODE DevModez;
 		EnumDisplaySettings(NULL,ENUM_CURRENT_SETTINGS,&DevModez);//获取当前的数据
 		DevModez.dmPelsWidth =SM_CXSCREEN_x;
 		DevModez.dmPelsHeight=SM_CYSCREEN_y;
 		ChangeDisplaySettings(&DevModez,CDS_UPDATEREGISTRY);//设置生效
 	}
}
```

### 调用

程序打开时 如 InitInstance() 调用 SetDevMode();  
程序退出时 如 ExitInstance() 调用 SetDevModeexit();
