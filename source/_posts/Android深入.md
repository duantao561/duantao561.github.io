---
title: Android深入
date: 2018-04-28 20:03:03
tags:
  - 工作随笔
  - Android
categories: 
  - 工作随笔
---

## 明天就放假了，同事宁神要走了。告诉我一些肺腑之言，发现自己有好多待掌握的东西。
### 1、socket
### 2、http  
	头  包体  表单（rfc1867）上传协议
### 3、java基础  
	java垃圾回收机制
	java存储分配机制
	Java各种集合  区别 使用  如何分配内存
	Java类加载机制
### 4、Android 
	View绘制原理
	自定义View
	动画
	binder机制 AIDL
	handler原理 looper使用（深入源码）
		HandlerThread结合intentService去看
### 5、图片加载、优化  （glide fresco）
	图片缓存策略：三级缓存 内存 文件 
	缓存回收策略：最久未使用、做不常使用。。。
	线程池
	glide对生命周期的控制fresco要好
<!-- more -->
### 6、网络库的封装
	线程池
	缓存策略
	参数，解析的封装
	常用网络库的源码（volley okhttp okgo）
### 7、组件化的构思
### 8、内存泄露的原因（长生命周期对象持有短生命周期对象的引用）以及优化
