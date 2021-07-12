## 1 Go开发环境

**下载链接**

[Download and install - The Go Programming Language (golang.org)](https://golang.org/doc/install)

**安装**

在linux下解压Go安装包到/usr/local/go目录下，并将/usr/local/go/bin加入到环境变量中。

**Go安装目录结构**

<img src="https://i.loli.net/2021/07/09/JfvtXUSFe4r9kcB.png" style="zoom:50%;" />

重要目录api、bin、doc、lib、misc、pkg、src、test

api：一组文本文件，保存Go每个版本的API的特色。

bin：编程生成的可执行文件，go和gofmt。

doc：网页文件，go的文档介绍。

lib：保存时区信息。

misc：杂七杂八的东西，go的插件。

pkg：平台相关目录（和目标操作系统相关），编译后生成的静态库文件。

src：go的源码文件，标准库文件。

test：go的测试文件。

其中最重要的三个文件夹就是src、bin和pkg。

**设置go get为国内源**

[Golang 笔记 | 国内 go get 用不了？其实很简单 (juejin.cn)](https://juejin.cn/post/6844904184064507917)

[goproxy/goproxy.cn: The most trusted Go module proxy in China. (github.com)](https://github.com/goproxy/goproxy.cn)

[七牛云 - Goproxy.cn](https://goproxy.cn/)

使用官方认证的go proxy（七牛云代理）

打开终端执行：

```
$ go env -w GO111MODULE=on
$ go env -w GOPROXY=https://goproxy.cn,direct
```

**go get的使用**

设置go get的下载目录GOPATH

```
export GOPATH=$HOME/gobook
```

## 2 Go论坛

1、Go语言中文网

[首页 - Go语言中文网 - Golang中文社区 (studygolang.com)](https://studygolang.com/)

内容非常丰富，第一大中文社区。

2、Golang官网

Go官方文档，权威，下面这个为中国区链接，可以直连。

[Documentation - The Go Programming Language (golang.org)](https://golang.org/doc/)

[Documentation - The Go Programming Language (google.cn)](https://golang.google.cn/doc/)

3、Github仓库

（1）使用Golang搭建网站

[astaxie/build-web-application-with-golang: A golang ebook intro how to build a web with golang (github.com)](https://github.com/astaxie/build-web-application-with-golang)

（2）中文版的awesome go，汇总了go开源项目

[hackstoic/golang-open-source-projects: 为互联网IT人打造的中文版awesome-go (github.com)](https://github.com/hackstoic/golang-open-source-projects#Web工具)

（3）Golang学习路线

[Alikhll/golang-developer-roadmap: Roadmap to becoming a Go developer in 2020 (github.com)](https://github.com/Alikhll/golang-developer-roadmap)

（4）Golang的小项目实现

[geektutu/7days-golang: 7 days golang programs from scratch (web framework Gee, distributed cache GeeCache, object relational mapping ORM framework GeeORM, rpc framework GeeRPC etc) 7天用Go动手写/从零实现系列 (github.com)](https://github.com/geektutu/7days-golang)

（5）Golang资料整合

[yangwenmai/learning-golang: Go 学习之路：Go 开发者博客、Go 微信公众号、Go 学习资料（文档、书籍、视频） (github.com)](https://github.com/yangwenmai/learning-golang)

（6）Golang面试题集合

[xiaobaiTech/golangFamily: 【超全golang面试题合集+golang学习指南+golang知识图谱+入门成长路线】 一份涵盖大部分golang程序员所需要掌握的核心知识。常用第三方库(mysql,mq,es,redis等)+机器学习库+算法库+游戏库+开源框架+自然语言处理nlp库+网络库+视频库+微服务框架+视频教程+音频音乐库+图形图片库+物联网库+地理位置信息+嵌入式脚本库+编译器库+数据库+金融库+电子邮件库+电子书籍+分词+数据结构+设计模式+去html tag标签等+go学习+go面试 (github.com)](https://github.com/xiaobaiTech/golangFamily)

4、极客兔兔的Go语言简明教程

主打快速上手

[Go 语言简明教程 | 快速入门 | 极客兔兔 (geektutu.com)](https://geektutu.com/post/quick-golang.html)

5、Go语言圣经

[前言 · Go语言圣经 (itsfun.top)](https://book.itsfun.top/gopl-zh/)

## 3 Go知识框架

1、Go基本语法

2、Go标准库和第三方库

3、Go web应用及框架

4、Go命令

## 4 Go学习路线

1、Go语言简明教程

初步掌握Go语言全貌

[Go 语言简明教程 | 快速入门 | 极客兔兔 (geektutu.com)](https://geektutu.com/post/quick-golang.html)

2、Go语言圣经

深入学习Go语言语法

[前言 · Go语言圣经 (itsfun.top)](https://book.itsfun.top/gopl-zh/)

