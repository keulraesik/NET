---
date: 2015-08-31 16:16:37
layout: post
title: "cocos2d-x & eclipse 环境配置"
categories: 编程
tags: cocos2d-x
---

## 文件下载

- [Android Development Tools](http://developer.android.com/sdk/installing/installing-adt.html)
- [Android SDK](https://developer.android.com/sdk/installing/index.html)（一般已含在`Android Development Tools`中）
- [Android NDK-r9d](http://developer.android.com/tools/sdk/ndk/index.html)
- [Java Development Kit-1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)


## cocos2d-x  
 
- 下载压缩包，并解压到开发路径 `E:\c2d-x\cocos2d-x-2.2.6`


## PATH配置

- ANDROID_SDK_ROOT  
`D:\Dev\Editors\adt-bundle-windows-x86-20140702\sdk`  
- ANDROID_NDK_ROOT  
`D:\Dev\Kits\android-ndk-r9d`
- COCOS2DX  
`E:\c2d-x\cocos2d-x-2.2.6`
- NDK_MODULE_PATH  
`%COCOS2DX%\cocos2dx\platform\third_party\android\prebuilt`  
- Add following to PATH  
`;%ANDROID_SDK_ROOT%\tools;%ANDROID_SDK_ROOT%\platform-tools;%ANDROID_ANDROID_NDK_ROOT%;%ANDROID_SDK_ROOT%\build-tools;%ANDROID_SDK_ROOT%\build-tools\19.1.0;%ANDROID_NDK_ROOT%;%ANDROID_SDK_ROOT%;%NDK_MODULE_PATH%`

## 创建项目

- 执行下面脚本创建`Project`  
```
cd %COCOS2DX%\tools\project-creator\
python create_project.py -project hello -package com.keulraesik.awesome -language cpp
```
- `project` 项目名  
- `package` 游戏主包名  
- `language` 使用编程语言 (`cpp, lua, js`)  

## 导入项目

- 菜单导入 `Import -> Existing Projects into Workspace`
- `%COCOS2DX%\projects\hello\`，选择项目 hello； 
- `%COCOS2DX%\cocos2dx\platform\android\` ，选择项目 libcocos2d
- 更改 project.properties `target=android-8` 为 `target=android-19`
- 引用 libcocos2d 为 hello 库项目, hello项目右键 `Android`/`Library` 处修改引用
- 将 `%COCOS2DX%\projects\hello\Resources\*` 拷贝至 `hello\assets` 
- hello 项目右键菜单 `C/C++ Build` / `Build command` 改为 `${NDK_ROOT}/ndk-build.cmd`
- 如果编译报错错误，请编辑 `hello/jni/Android.mk` 在 `include $(BUILD_SHARED_LIBRARY)` 之后添加  
```
$(call import-add-path, $(COCOS2DX))  
$(call import-add-path, $(COCOS2DX)\cocos2dx\platform\third_party\android\prebuilt)  
```
- 项目 cocos2dx, scripting, extensions, Classes path invalid fix  
```  
在hello项目右键    
Resource -> Linked Resources -> Path Variables    
添加 COCOS2DX=E:\c2d-x\cocos2d-x-2.2.6
```

## 最后

现在你的`Hello Project`应该可以正常编译与运行了，此方法仅限于 `cocos2dx-2.x` 系列。
部分配置涉及到具体软件版本，请根据你使用的版本适配
