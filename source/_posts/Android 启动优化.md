---
title: Android启动优化
date: 2018-08-18 15:03:03
tags:
  - 工作随笔
  - Android
categories: 
  - 工作随笔
---

## Android 启动优化

### 1.首先定义一个drawable 用于设置主题背景（android:windowBackground）
```
<?xml version="1.0" encoding="utf-8"?>
<layer-list
    android:opacity="opaque"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@color/white"/>
    <item >
        <bitmap android:src="@drawable/icon_logo"
            android:gravity="center"/>
    </item>
</layer-list>
```
### 2.设置启动页主题背景（android:windowBackground）
```
    <style name="app_cool_launch" parent="@style/Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowBackground">@drawable/bg_cool_launch_img</item>
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowAnimationStyle">@style/notAnimation</item>
    </style>
```
------
> * 默认情况下，所有可绘制项都会缩放以适应包含视图的大小。因此，将图像放在图层列表中的不同位置可能会增大视图的大小，并且有些图像会相应地缩放。为避免缩放列表中的项目，请在 < item> 元素内使用 < bitmap> 元素指定可绘制对象，并且对某些不缩放的项目（例如 “center”）定义重力。例如，以下 < item> 定义缩放以适应其容器视图的项目：
```
    <item android:drawable="@drawable/image" />
```
> *为避免缩放，以下示例使用重力居中的 元素：
```
    <item>
        <bitmap android:src="@drawable/image"
            android:gravity="center" />
    </item>
```
