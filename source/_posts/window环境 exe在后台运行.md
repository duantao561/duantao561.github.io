---
title: window环境 exe在后台运行
date: 2019-7-24 13:03:03
tags:
  - 学习笔记
  - 系统
categories: 
  - 学习笔记
---

# 2019-7-24

## 1.window环境 exe在后台运行
[Windows下程序后台执行文件](https://blog.csdn.net/lendq/article/details/80283268) 

<!-- more -->

 - .bat文件

```
@echo off
if "%1"=="h" goto begin
start mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
:begin
xxxxx 要执行的命令 
```

```
"%~nx0 h",0中的%~nx0是把批处理自己的文件名传送给vbs，以便让vbs隐藏打开它。h是设置隐藏属性，0为隐藏运行。window.close是关闭窗口（可以说是关闭vbs）。  不加if "%1" == "h" goto begin会导致崩溃是因为要检查批处理是否隐藏了，如果隐藏则跳到“begin”（中文名为“开始”）执行。不然的话系统就会以为批处理没有隐藏，没有返回结果而不停地工作，调用程序。
```
- .vbs文件  
 保存成.vbs文件，直接运行.vbs文件即可实现后台运行。

```
set wscriptObj = CreateObject("Wscript.Shell")   
wscriptObj.run "xxx要执行的命令",0  
```
- 开机自启动
 将.vbs文件的快捷方式 复制到如下目录  
 C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp
 * 这种方式只能是系统登陆以后，进入桌面才会启动

[小小分享 偷偷在后台运行程序vbs](https://blog.csdn.net/szjy8/article/details/83297408) 


## 2. 一些命令
  1. rm -rf /data  会删掉data目录以及子目录下的所有文件 （慎用，文件名一定要搞对，所删除的文件，一般都不能恢复！）
  2. Linux下的tar压缩解压缩命令详解
  
  ```
	tar
	-c: 建立压缩档案
	-x：解压
	-t：查看内容
	-r：向压缩归档文件末尾追加文件
	-u：更新原压缩包中的文件
	
	这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。
	===================================
	-z：有gzip属性的
	-j：有bz2属性的
	-Z：有compress属性的
	-v：显示所有过程
	-O：将文件解开到标准输出
	===================================
	下面的参数-f是必须的
	-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。
	# tar -cf all.tar *.jpg
	这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。
	# tar -rf all.tar *.gif
	这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。
	# tar -uf all.tar logo.gif
	这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。
	# tar -tf all.tar
	这条命令是列出all.tar包中所有文件，-t是列出文件的意思
	# tar -xf all.tar
	这条命令是解出all.tar包中所有文件，-t是解开的意思
	===================================
	压缩
	tar -cvf jpg.tar *.jpg //将目录里所有jpg文件打包成jpg.tar 
	tar -czf jpg.tar.gz *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz
	tar -cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2
	tar -cZf jpg.tar.Z *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z
	rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux
	zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux
	===================================
	解压
	tar -xvf file.tar //解压 tar包
	tar -xzvf file.tar.gz //解压tar.gz
	tar -xjvf file.tar.bz2   //解压 tar.bz2
	tar -xZvf file.tar.Z   //解压tar.Z
	unrar e file.rar //解压rar
	unzip file.zip //解压zip
	===================================
	总结
	1、*.tar 用 tar -xvf 解压
	2、*.gz 用 gzip -d或者gunzip 解压
	3、*.tar.gz和*.tgz 用 tar -xzf 解压
	4、*.bz2 用 bzip2 -d或者用bunzip2 解压	
	5、*.tar.bz2用tar -xjf 解压
	6、*.Z 用 uncompress 解压
	7、*.tar.Z 用tar -xZf 解压
	8、*.rar 用 unrar e解压
	9、*.zip 用 unzip 解压
  ```
  3. [手把手教你破解微信本地数据库(利用Sqlcipher查看)](https://blog.csdn.net/qq_30548105/article/details/72676245)  
  [使用微信聊天记录统计信息](https://notes.zz-zigzag.com/2017/09/wechat-db.html)  
  [如何备份微信的聊天记录？](https://www.zhihu.com/question/19924224)
  [Mac终端使用Sqlcipher加解密基础过程详解](https://blog.csdn.net/u011195398/article/details/85266214)  
  
4. [全面总结： Golang 调用 C/C++，例子式教程](https://www.cnblogs.com/linguanh/p/8323487.html)
5. [Go实现海量日志收集系统](https://blog.csdn.net/u011596455/article/details/80073841)
6. [超强内网穿透nps 解决所有无公网IP问题](https://imgki.com/archives/62.html)
 
