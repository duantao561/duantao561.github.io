---
title: log4j使用 && Intellij Idea打jar包
date: 2019-8-1 13:03:03
tags:
  - 学习笔记
  - java
categories: 
  - 学习笔记
---

# 一、log4j 使用
- 首先引入log4j

```
<!-- log4j -->
<dependency>
	<groupId>log4j</groupId>
	<artifactId>log4j</artifactId>
	<version>1.2.16</version>
</dependency>
```
- 编辑配置文件 log4j.properties

```
#日志级别,输出目的地  
log4j.rootLogger=DEBUG,stdout,logFile

### 输出信息到控制抬 ###
log4j.appender.stdout = org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target = System.out
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l]: %m%n

##logFile log
log4j.appender.logFile = org.apache.log4j.FileAppender
log4j.appender.logFile.layout = org.apache.log4j.PatternLayout
log4j.appender.logFile.layout.ConversionPattern = [%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l]: %m%n
log4j.appender.logFile.Threshold = DEBUG
log4j.appender.logFile.ImmediateFlush = TRUE
log4j.appender.logFile.Append = TRUE
log4j.appender.logFile.File = ./local_files/logs/${log.file}
log4j.appender.logFile.Encoding = UTF-8

#CommonLog log
log4j.logger.CommonLog=INFO,CommonLog,CommonStdout
#如果additivity设置为false  就不想父logger打印
log4j.additivity.CommonLog = false

log4j.appender.CommonStdout = org.apache.log4j.ConsoleAppender
log4j.appender.CommonStdout.Target = System.out
log4j.appender.CommonStdout.layout = org.apache.log4j.PatternLayout
log4j.appender.CommonStdout.layout.ConversionPattern=[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l]: %m%n


log4j.appender.CommonLog =org.apache.log4j.DailyRollingFileAppender
#log4j.appender.CommonLog.File= ./local_files/logs/common_log.txt
log4j.appender.CommonLog.File= ./local_files/logs/${common_log.file}
#log4j.appender.CommonLog.File= ${log.dir}/${common_log.file}
#System.setProperty(“log.dir”, logDir);
#System.setProperty(“common_log.file”, infoLogFileName);
log4j.appender.CommonLog.DatePattern='_'yyyy-MM-dd-HH'.txt'
#log4j.appender.CommonLog.Threshold=INFO
log4j.appender.CommonLog.layout=org.apache.log4j.PatternLayout
log4j.appender.CommonLog.layout.ConversionPattern=[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l] : %m%n

#ExceptionLog log
log4j.logger.ExceptionLog=INFO,ExceptionLog,ExceptionStdout
log4j.additivity.ExceptionLog = false

log4j.appender.ExceptionStdout = org.apache.log4j.ConsoleAppender
log4j.appender.ExceptionStdout.Target = System.out
log4j.appender.ExceptionStdout.layout = org.apache.log4j.PatternLayout
log4j.appender.ExceptionStdout.layout.ConversionPattern=[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l]: %m%n


log4j.appender.ExceptionLog =org.apache.log4j.DailyRollingFileAppender
log4j.appender.ExceptionLog.File= ./local_files/logs/${exception_log.file}
#log4j.appender.ExceptionLog.File= ./local_files/logs/exception_log.txt
log4j.appender.ExceptionLog.DatePattern='_'yyyy-MM-dd-HH'.txt'
#log4j.appender.ExceptionLog.Threshold=INFO
log4j.appender.ExceptionLog.layout=org.apache.log4j.PatternLayout
log4j.appender.ExceptionLog.layout.ConversionPattern=[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l] : %m%n
#[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l][%c] : %m%n
#[%-5p][%d{yyyy-MM-dd HH:mm:ss}] [%l] : %m%n
```
- 使用方法

```
public static Logger getCommonLogger(){
    if (null == commonLogger){
        System.setProperty("log.file", getLogName());
        System.setProperty("common_log.file", getCommonLogName());
        System.setProperty("exception_log.file", getExceptionLogName());
	  //如果没有放到默认路径下，则需要如下加载方式
	  //PropertyConfigurator.configure("log4j.properties");
        commonLogger = Logger.getLogger("CommonLog");
        if (IS_DEV){
            commonLogger.setLevel(Level.DEBUG);
        }else {
            commonLogger.setLevel(Level.INFO);
        }

    }
    return commonLogger;
}

//这样调用
//MyLogger.getCommonLogger().debug("getCommonLogger");

```



## 问题
### 1. 解决log4j.properties不起作用的问题
1. 如果没有放到默认路径下，则需要如下加载方式
	PropertyConfigurator.configure("log4j.properties");
2. 在main文件夹下创建resources文件夹，将log4j.properties放到该文件夹下解决

### 2. 解决log4j.properties打不到jar包中的问题
1. 同样是因为没有放到默认的路径中
2. 在main文件夹下创建resources文件夹，将log4j.properties放到该文件夹下解决

# 二、Intellij idea  打jar包
- 在File -> project Structure （command+；）->选择Artifacts->点击＋    
  -> 选择jar  ->  选择From modules with Dependencies.

- 选择执行的主类 main class：   
选择“extract to the target jar”，即把引用第三方的jar文件，同时打包到jar里。

- 配置“Directory for META-INF/MAINFEST.MF”      
**需要改成：项目根目录！！！项目根目录！！！项目根目录！！！（反正不能放在原来默认的目录下面）**如果根目录已经有了，就删掉

```
具体配置详细：
Module： 模块，选择需要打包的模块。如果程序没有分模块，那么只有一个可以选择的。
MainClass：选择程序的入口类。
extract to the target JAR：抽取到目标JAR。选择该项则会将所依赖的jar包全都打到一个jar文件中。
copy to the output directory and link via manifest：将依赖的jar复制到输出目录并且使用manifest链接它们。
Direct for META-INF/MANIFEST.MF： 如果上面选择了 "copy to ... "这一项，这里需要选择生成的manifest文件在哪个目录下。
Include tests： 是否包含tests。 一般这里不选即可。
```
- 点击ok进入下一步
- 此页直接点击apply-->ok即可（name是jar包名字，output directory是jar包生成的地址，type是类型）
- 点击Build ---> Build Artifacts..  --->  Build 即可执行打包命令
- 最后在此目录下找到打好的jar包。
- 运行java -jar xxxx.jar 命令即可。
