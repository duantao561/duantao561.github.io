---
title: Golang 配置
date: 2019-7-18 13:03:03
tags:
  - 学习笔记
  - Go
categories: 
  - 学习笔记
---

# 学习1

### 2019-7-18

1. 重复的事情进行思考总结，磨刀不误砍柴工！

	```
	gotest
	gotest
	gotest
	```

<!-- more -->

### 2019-7-19
1. 在 go.mod 文件下面添加如下可替换本地库


	```
	replace golang.org/x/crypto => ../golang.org/x/crypto
	
	replace golang.org/x/sync => ../golang.org/x/sync
	
	replace golang.org/x/net => ../golang.org/x/net
	
	replace golang.org/x/sys => ../golang.org/x/sys
	
	replace golang.org/x/text => ../golang.org/x/text
	
	replace golang.org/x/tools => ../golang.org/x/tools
	
	```

2. 替换远程

	```
	replace (
		cloud.google.com/go => github.com/googleapis/google-cloud-go v0.34.0
		github.com/go-tomb/tomb => gopkg.in/tomb.v1 v1.0.0-20141024135613-dd632973f1e7
		go.opencensus.io => github.com/census-instrumentation/opencensus-go v0.19.0
		go.uber.org/atomic => github.com/uber-go/atomic v1.3.2
		go.uber.org/multierr => github.com/uber-go/multierr v1.1.0
		go.uber.org/zap => github.com/uber-go/zap v1.9.1
		golang.org/x/crypto => github.com/golang/crypto v0.0.0-20181001203147-e3636079e1a4
		golang.org/x/lint => github.com/golang/lint v0.0.0-20181026193005-c67002cb31c3
		golang.org/x/net => github.com/golang/net v0.0.0-20180826012351-8a410e7b638d
		golang.org/x/oauth2 => github.com/golang/oauth2 v0.0.0-20180821212333-d2e6202438be
		golang.org/x/sync => github.com/golang/sync v0.0.0-20181108010431-42b317875d0f
		golang.org/x/sys => github.com/golang/sys v0.0.0-20181116152217-5ac8a444bdc5
		golang.org/x/text => github.com/golang/text v0.3.0
		golang.org/x/time => github.com/golang/time v0.0.0-20180412165947-fbb02b2291d2
		golang.org/x/tools => github.com/golang/tools v0.0.0-20181219222714-6e267b5cc78e
		google.golang.org/api => github.com/googleapis/google-api-go-client v0.0.0-20181220000619-583d854617af
		google.golang.org/appengine => github.com/golang/appengine v1.3.0
		google.golang.org/genproto => github.com/google/go-genproto v0.0.0-20181219182458-5a97ab628bfb
		google.golang.org/grpc => github.com/grpc/grpc-go v1.17.0
		gopkg.in/alecthomas/kingpin.v2 => github.com/alecthomas/kingpin v2.2.6+incompatible
		gopkg.in/mgo.v2 => github.com/go-mgo/mgo v0.0.0-20180705113604-9856a29383ce
		gopkg.in/vmihailenco/msgpack.v2 => github.com/vmihailenco/msgpack v2.9.1+incompatible
		gopkg.in/yaml.v2 => github.com/go-yaml/yaml v0.0.0-20181115110504-51d6538a90f8
		labix.org/v2/mgo => github.com/go-mgo/mgo v0.0.0-20160801194620-b6121c6199b7
		launchpad.net/gocheck => github.com/go-check/check v0.0.0-20180628173108-788fd7840127
	)

	主要包括:
	golang.org
	google.golang.org
	gopkg.in
	go.uber.org
	cloud.google.com在下载包时会有timeout 导致编译失败，以上是对应的github的库
	```
3. redis 外网无法访问的问题
	* 安装完以后，需要打开6379端口
	* redis-server默认开放的127.0.0.1 IP地址需要修改为0.0.0.0才可以被其他机器访问
		* 1、在Redis安装目录下找到配置文件 redis.config
		* 2、修改 bind 127.0.0.1 改为 bind 0.0.0.0 
		* 3、重启Redis服务

4. 学习golang的一些知名库
	* Logrus (go get github.com/sirupsen/logrus)
	
		```
		package main

		import (
		  log "github.com/sirupsen/logrus"
		)
		func init() {
			log.SetFormatter(&log.JSONFormatter{
				PrettyPrint: false,
			})
			log.SetLevel(log.InfoLevel)
		}
		func main() {
		  log.WithFields(log.Fields{
		    "animal": "walrus",
		  }).Info("A walrus appears")
		}
		```
	* yaml (go get gopkg.in/yaml.v2)
	
		```
		host: localhost:3306
		user: root
		pwd: 123456
		dbname: test
		Redis:
		  Addr: 140.143.224.224:6379 # redis链接
		  Password:   #redis 密码
		```
	
		```
		package main

		import (
		    "io/ioutil"
		    "gopkg.in/yaml.v2"
		    "fmt"
		)
		
		func main() {
		   var c conf
		   conf:=c.getConf()
		   fmt.Println(conf.Host)
		}
		
		//profile variables
		type conf struct {
		    Host string `yaml:"host"`
		    User string `yaml:"user"`
		    Pwd string `yaml:"pwd"`
		    Dbname string `yaml:"dbname"`
		    // redis
			Redis struct {
				Addr     string `yaml:"Addr"`     // redis链接
				Password string `yaml:"Password"` //redis 密码
			} `yaml:"Redis"`
		}
		func (c *conf) getConf() *conf {
		    yamlFile, err := ioutil.ReadFile("conf.yaml")
		    if err != nil {
		        fmt.Println(err.Error())
		    }
		    err = yaml.Unmarshal(yamlFile, c)
		    if err != nil {
		        fmt.Println(err.Error())
		    }
		    return c
		}
		```
	
5. scss文件转换css 
	- https://www.sass.hk/install/
		- 命令 sass --watch inputdir:outputdir
6. vscode setting.json

	```
	{
    "java.errors.incompleteClasspath.severity": "ignore",
    "window.zoomLevel": 1,
    "editor.minimap.enabled": false,
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
    "git.autofetch": false,
    "files.autoSave": "afterDelay",
    "java.configuration.checkProjectSettingsExclusions": false,
    "editor.wordWrap": "on",
    //===============go setting=======================
    // "go.formatTool": "goimports",
    "go.inferGopath": false,
    "go.buildOnSave": "workspace",
    "go.lintOnSave": "package",
    "go.vetOnSave": "package",
    "go.buildTags": "",
    "go.buildFlags": [],
    "go.lintFlags": ["--disable=all", "--enable=errcheck"],
    "go.vetFlags": [],
    "go.coverOnSave": false,
    "go.useCodeSnippetsOnFunctionSuggest": false,
//     "go.formatOnSave": true,
    "go.formatTool": "goreturns",
    "go.goroot": "/usr/local/go",
    "go.gocodeAutoBuild": false,
    "go.useLanguageServer": true
//     "go.alternateTools": {
//       "go-langserver": "gopls", 
//     }
//     "go.languageServerExperimentalFeatures": {
//       "format": true,
//       "autoComplete": true
//     },
//     "[go]": {
//         "editor.codeActionsOnSave": {
//             "source.organizeImports": true
//         },
//     }
}
	
	环境变量设置：
	export GO111MODULE=on
	```
7. go build
	
	```
	Golang 支持在一个平台下生成另一个平台可执行程序的交叉编译功能。
	
	
	Mac下编译Linux, Windows平台的64位可执行程序：
	
	
	CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build test.go
	CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build test.go
	Linux下编译Mac, Windows平台的64位可执行程序：
	
	
	CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build test.go
	CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build test.go
	Windows下编译Mac, Linux平台的64位可执行程序：
	
	
	SET CGO_ENABLED=0
	SET GOOS=darwin3
	SET GOARCH=amd64
	go build test.go
	
	
	SET CGO_ENABLED=0
	SET GOOS=linux
	SET GOARCH=amd64
	go build test.go
	 
	
	
	GOOS：目标可执行程序运行操作系统，支持 darwin，freebsd，linux，windows
	GOARCH：目标可执行程序操作系统构架，包括 386，amd64，arm
	```