[Go Gin 简明教程 | 快速入门 | 极客兔兔 (geektutu.com)](https://geektutu.com/post/quick-go-gin.html)

## Go简明教程

1、3.3 字符串的例子没怎么看懂

2、切片和字典都可以用make函数来初始化

3、if语句的判断条件中可以插入赋值语句

4、Go语言使用const常量模拟枚举

5、Go语言的switch不需要break

6、Go语言的for函数经常使用for range遍历

7、函数返回值可以命名，简化return

8、可预知的错误为error，不可预知的为panic

9、Go中使用defer和recover来代替try, catch。defer定义异常处理的函数，如果触发了panic，控制权就交给的defer

10、结构体使用name{field : value}的形式创建实例

11、可以使用new对结构体实现初始化

12、Go语言中实现接口，不需要显式声明，只需要实现该接口对应的方法

13、将空值转换为具体类型，再转换为接口，可以检测该类型是否实现了接口

14、空接口可以表示任意类型

15、并发协程不需要通信时，使用sync.WaitGroup等待所有并发协程执行结束

16、channel信道可以在协程之间传递消息，使用<-符号传递信息，信道使用make(chan string, 10)来创建

17、单元测试为_test.go文件（约定），运行go test时自动运行当前package下的所有测试用例。

18、一般一个文件夹一个package。

19、首字母大写时public的，对其他package可见。

20、Go Modules是包管理工具，使用 go mod初始化module，生成go.mod文件，记录当前模块的模块名和所有依赖包的版本

21、导入模块：import 模块名/子目录名

 

## Go Gin简明教程

1、Go语言有大量的辅助工具，如果使用vscode，将会提示安装必要的工具，如静态检查、自动补全等。

2、安装Gin：直接使用go get

3、如何写Gin：导入gin包，使用gin.Default生成实例，用该实例声明路由，告诉gin什么样的url能触发传入的函数，调用实例的Run方法启动应用。

4、gin的路由方法包括GET,POST,PUT,PATCH,DELETE和OPTIONS，以及Any。

5、动态路由：使用Param、Query匹配不同的url。

 

## Go2 新性能简明教程

1、Go语言原生支持Goroutine和Channel，极大地降低了并发和异步编程的复杂度。

2、Go2 较大的改动：切片操作，for语言加强，类型别名

3、Go2 设计草案-错误处理：引入handle err和check关键词，减少错误if判断

4、Go2 设计草案-错误值：为error定义一个可选接口Unwrap，用来返回错误链上的下一个错误；定义可选接口Fomat，返回错误信息。

5、Go2 设计草案-泛型

 

## Go Protobuf简明教程

1、protobuf：结构化数据存储格式

2、Protobuf 在 `.proto` 定义需要处理的结构化数据，可以通过 `protoc` 工具，将 `.proto` 文件转换为 C、C++、Golang、Java、Python 等多种语言的代码，兼容性好，易于使用。

3、使用protobuf，首先要下载安装protoc。

4、在 Golang 中使用 protobuf，还需要安装 protoc-gen-go，这个工具用来将 `.proto` 文件转换为 Golang 代码。



## 问题

1、查看有关Go的环境变量

```
go env
```

重要的环境变量有GOROOT和GOPATH

