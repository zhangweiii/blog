---
title: Hello Golang
date: 2020-04-23
categories: Go学记
tags: Go学记
comments: true
img:
---

## Golang 语言特点

Golang是编译型语言，特点简单和快，有着类似`Python`的简洁易编写和类似`C++`的运行速度。可跨平台编译，高效率的协程和简单的通道，使得高并发程序简单又高效。以下是Golang版的`Hello World`


## 第一个Golang程序

``` GO
package main  // 声明包名main

import "fmt"  // 导入golang标准库包fmt

func main() { // main函数，程序入口
    fmt.Println("Hello World!")  // 打印
}
```

一个可直接运行的Golang程序必须有`main`包和`main`函数，否则会报以下错误

``` BASH
# 以下是没有main包报的错误
go run: cannot run non-main package

# 以下是没有main函数报的错误
# command-line-arguments
runtime.main_main·f: function main is undeclared in the main package
```

## 执行Golang程序

假设将它保存为`hello.go`，要使它运行，命令行键入`go run hello.go`，程序会输出

``` BASH
Hello World!
```

> 你也可以到这里亲自运行一下看看[play.studygolang.com](https://play.studygolang.com/p/4em_C0unFEW)

你也可以编译成二进制可执行程序，执行以下命令编译

``` BASH
go build hello.go
```

执行后，同级目录下会多一个`hello`可执行程序，输入以下命令执行这个程序

``` BASH
./hello
```

程序输出结果会和`go run`命令结果一样

## 交叉编译

你还可以进行交叉编译，就比如Mac平台编译为Linux平台的可执行程序，分别有以下命令

``` BASH
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go     # Mac 编译成 Linux 执行程序
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go   # Mac 编译成 Windows 执行程序

CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go    # Linux 编译成 Mac 执行程序
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go   # Linux 编译成 Windows 执行程序

# Windows 编译成 Mac 执行程序
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go

# Windows 编译成 Linux 执行程序
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```

`CGO_ENABLED=0`是禁用CGO，因为交叉编译不支持
`GOOS`是指定目标平台，分别有darwin/freebsd/linux/windows
`GOARCH`是指目标平台的架构，有386/amd64/arm等

## 包、main函数、init函数

多说一下，包就是其它语言库或模块，一般包名和文件夹名字统一，包下有一些`.go`源码文件，包中变量或函数首字母大写为`public`，也就是包外可以使用。`main`函数就是入口函数，值得一说的是每个包里都可以有一个或多个`init`函数，`init`执行顺序会优先于`main`函数，多个`init`会顺序执行，示例代码如下

``` GO
package main

import (
	"fmt"
)

func init() {
	fmt.Println("First init function called")
}

func init() {
	fmt.Println("Secend init function called")
}

func main() {
	fmt.Println("Main function called")
}
```

执行结果

``` BASH
First init function called
Secend init function called
Main function called
```

> 你也可以到这里亲自运行一下看看[play.studygolang.com](https://play.studygolang.com/p/1v2U-azVuVp)

