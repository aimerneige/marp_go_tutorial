---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
# backgroundImage: url('https://marp.app/assets/hero-background.jpg')
backgroundImage: url(image/background/hero-background.jpg)
marp: true
# header: "**AimerNeige** (C) All Rights Reserved"
# footer: "**AimerNeige**"
---

<!-- _class: lead -->

# **Go 语言基础入门**

---

![bg left:40% 80%](./image/biplane.svg)


# **Golang 简单介绍**

- Golang 是由谷歌开发的编程语言。
- 官方网站 <https://go.dev/>

---

# 优点：

1. 可以直接编译为机器码，有更高性能同时编译速度极快。
2. 静态类型语言，在编译时就能检查出很多问题。
3. 语义级异步，强大的 goroutines 和 channel。
4. 支持垃圾回收，无需考虑内存泄漏问题。
5. 丰富的标准库，尤其在网络方面的库非常强大。
6. 官方提供的完整工具链，比如 gofmt，完美统一了代码格式。
7. 支持跨平台编译。
8. 内嵌的 C 语言支持。

---

# 缺点

1. ~~没有泛型~~ [go 1.18 已经支持了泛型](https://go.dev/blog/go1.18)
2. 糟糕的错误处理。`if err != nil { return err }`
3. 不完整的面向对象。
4. 没有真枚举。
5. `interface{}` 实际上就是 C 语言中的 `void *`
6. 采用大写命名法来标记公共或私有变量。
7. 非常容易写出大量重复代码。
8. 不允许循环引用。
9. 语言较新。

---

# Go 适合干什么

- 服务器编程，替代 C/C++。
  - 处理日志、数据打包、虚拟机处理、文件系统等。
- 分布式系统，数据库代理器。
- 网络编程。
  - Web 应用，Web API，gRpc
- 微服务。

---

# 配置开发环境

## <https://aimerneige.com/zh/post/go-env-setup-for-beginner/>

---

# Hello World

`main.go`

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, 世界")
}
```

```bash
go run main.go
```

---

# 声明

- var
- const
- type
- func

---

# 变量

```go
var 变量名字 类型 = 表达式
```

```go
var pi float64 = 3.14
```

```go
var name string
```

---

# 赋值

显示指明类型

```go
var name string
name = "Aimer Neige"
```

类型推断

```go
name := "Aimer Neige"
```

```go
-= += *= /=
++ --
```

---

# 类型

```go
type 类型名字 底层类型
```

```go
type myFloat float64
```

```go
type myStruct struct {
    ...
}
```

---

# 包

```go
import (
    "fmt"
    "go-tutorial/add"
    ...
)
```

---

# 作用域

```go
func main() {
    x := "hello!"
    for i := 0; i < len(x); i++ {
        x := x[i]
        if x != '!' {
            x := x + 'A' - 'a'
            fmt.Printf("%c", x) // "HELLO" (one letter per iteration)
        }
    }
}
```

---

```go
func main() {
    x := "hello"
    for _, x := range x {
        x := x + 'A' - 'a'
        fmt.Printf("%c", x) // "HELLO" (one letter per iteration)
    }
}
```

```go
if x := f(); x == 0 {
    fmt.Println(x)
} else if y := g(x); x == y {
    fmt.Println(x, y)
} else {
    fmt.Println(x, y)
}
fmt.Println(x, y) // compile error: x and y are not visible here
```

---

```go
if f, err := os.Open(fname); err != nil { // compile error: unused: f
    return err
}
f.ReadByte() // compile error: undefined f
f.Close()    // compile error: undefined f
```

```go
f, err := os.Open(fname)
if err != nil {
    return err
}
f.ReadByte()
f.Close()
```

---

```go
var cwd string

func init() {
    cwd, err := os.Getwd() // compile error: unused: cwd
    if err != nil {
        log.Fatalf("os.Getwd failed: %v", err)
    }
}
```

```go
var cwd string

func init() {
    cwd, err := os.Getwd() // NOTE: wrong!
    if err != nil {
        log.Fatalf("os.Getwd failed: %v", err)
    }
    log.Printf("Working directory = %s", cwd)
}
```

---

```go
var cwd string

func init() {
    var err error
    cwd, err = os.Getwd()
    if err != nil {
        log.Fatalf("os.Getwd failed: %v", err)
    }
}
```

---

# 基础数据类型

- 整型
- 浮点数
- 复数
- 布尔型
- 字符串
- 常量

---

# 复合数据类型

- 数组
- Slice（切片）
- Map（哈希表）
- 结构体
- JSON
- 文本和HTML模板

---

# 函数

- 函数声明
- 递归
- 多返回值
- 错误
- 函数值

---

# 函数

- 匿名函数
- 可变参数
- Deferred函数
- Panic异常
- Recover捕获异常

---

# 方法

- 方法声明
- 基于指针对象的方法
- 通过嵌入结构体来扩展类型
- 方法值和方法表达式
- 封装

---

# 接口

- 接口是合约
- 接口类型
- 实现接口的条件
- 接口值
- error接口

---

参考资料

- <https://yar999.gitbook.io/gopl-zh/>