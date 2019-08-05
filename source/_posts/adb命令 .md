---
title: adb命令
date: 2019-7-17 13:03:03
tags:
  - 工作随笔
  - Android
categories: 
  - 工作随笔
---

# adb命令 

### 2019-7-17
1. 打开scheme
 - adb shell am start -a android.intent.action.VIEW -d qqnews://article_9527?nm=20180808A083TK00
2. 查看当前页面的activity
 - `windows下:` adb shell dumpsys activity | findstr mFocus  
 - `mic 或者 linux下:` adb shell dumpsys activity | grep mFocus  
<!-- more -->
3. 点击返回按钮
 - adb shell input keyevent 4
4. home键的点击
 - adb shell input keyevent 3
5. 获取当前页面内容
 - adb shell uiautomator dump
6. 单击指定的点(300,450)
 - adb shell input tap 300 450
7. 滑动当前页面(最后一个参数是时间毫秒)
 - adb shell input swipe 360 920 360 280 500
8. 进入指定页面(activity)
 - adb shell am start -n com.ss.android.article.news/com.ss.android.article.news.activity.MainActivity
9. 切换到adbkeyboard输入法
 - adb shell ime set com.android.adbkeyboard/.AdbIME
10. adb端口重定向
 - adb forward tcp:59254 tcp:7912




 
	