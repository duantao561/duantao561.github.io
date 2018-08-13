---
title: Android����
date: 2018-08-18 15:03:03
tags:
  - �������
  - Android
categories: 
  - �������
---

## Android �����Ż�

### 1.���ȶ���һ��drawable �����������ⱳ����android:windowBackground��
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
### 2.��������ҳ���ⱳ����android:windowBackground��
```
    <style name="app_cool_launch" parent="@style/Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowBackground">@drawable/bg_cool_launch_img</item>
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowAnimationStyle">@style/notAnimation</item>
    </style>
```
------
> * Ĭ������£����пɻ��������������Ӧ������ͼ�Ĵ�С����ˣ���ͼ�����ͼ���б��еĲ�ͬλ�ÿ��ܻ�������ͼ�Ĵ�С��������Щͼ�����Ӧ�����š�Ϊ���������б��е���Ŀ������ < item> Ԫ����ʹ�� < bitmap> Ԫ��ָ���ɻ��ƶ��󣬲��Ҷ�ĳЩ�����ŵ���Ŀ������ ��center�����������������磬���� < item> ������������Ӧ��������ͼ����Ŀ��
```
    <item android:drawable="@drawable/image" />
```
> *Ϊ�������ţ�����ʾ��ʹ���������е� Ԫ�أ�
```
    <item>
        <bitmap android:src="@drawable/image"
            android:gravity="center" />
    </item>
```