---
title: Go
date: 2020-12-17 21:51:44
background: bg-[#4ba4cc]
tags:
    - Go
categories:
    - 编程
intro: |
    本速查表提供了基本语法和方法，以帮助您使用 [Go](https://go.dev/)。
plugins:
    - copyCode
    - runCode
---

## 入门

### hello.go

```go
package main

import "fmt"

func main() {
        fmt.Println("你好，世界！")
}
```

直接运行

```shell script
$ go run hello.go
你好，世界！
```

或者在 [Go repl](https://repl.it/languages/go) 中尝试

### 变量

```go
var s1 string
s1 = "学习 Go！"

// 一次声明多个变量
var b, c int = 1, 2
var d = true
```

短声明

```go
s1 := "学习 Go！"        // 字符串
b, c := 1, 2             // 整数
d := true                // 布尔值
```

参见：[Go 基本类型](#go-基本类型)

### 函数

```go
package main

import "fmt"

// 程序的入口点
func main() {
        fmt.Println("你好，世界！")
        say("你好 Go！")
}

func say(message string) {
        fmt.Println("你说：", message)
}
```

参见：[函数](#go-函数)

### 注释

```go
// 单行注释

/* 多行
     注释 */
```

### If 语句

```go
if true {
        fmt.Println("是的！")
}
```

参见：[流程控制](#go-流程控制)

## Go 基本类型

### 字符串

```go
s1 := "你好" + "世界"

s2 := `一个“原始”字符串字面量
可以包含换行符。`

// 输出：10
fmt.Println(len(s1))

// 输出：你好
fmt.Println(string(s1[0:5]))
```

字符串的类型是 `string`。

### 数字

```go
num := 3         // int
num := 3.        // float64
num := 3 + 4i    // complex128
num := byte('a') // byte (uint8 的别名)

var u uint = 7        // uint (无符号)
var p float32 = 22.7  // 32 位浮点数
```

#### 运算符

```go
x := 5
x++
fmt.Println("x + 4 =", x + 4)
fmt.Println("x * 4 =", x * 4)
```

参见：[更多运算符](#go-运算符和标点符号)

### 布尔值

```go
isTrue   := true
isFalse  := false
```

#### 运算符

```go
fmt.Println(true && true)   // true
fmt.Println(true && false)  // false
fmt.Println(true || true)   // true
fmt.Println(true || false)  // true
fmt.Println(!true)          // false
```

参见：[更多运算符](#go-运算符和标点符号)

### 数组 {.row-span-2}

```go
┌────┬────┬────┬────┬─────┬─────┐
| 2  | 3  | 5  | 7  | 11  | 13  |
└────┴────┴────┴────┴─────┴─────┘
    0    1    2    3     4     5
```

---

```go
primes := [...]int{2, 3, 5, 7, 11, 13}
fmt.Println(len(primes)) // => 6

// 输出：[2 3 5 7 11 13]
fmt.Println(primes)

// 与 [:3] 相同，输出：[2 3 5]
fmt.Println(primes[0:3])
```

---

```go
var a [2]string
a[0] = "你好"
a[1] = "世界"

fmt.Println(a[0], a[1]) //=> 你好 世界
fmt.Println(a)   // => [你好 世界]
```

#### 二维数组

```go
var twoDimension [2][3]int
for i := 0; i < 2; i++ {
        for j := 0; j < 3; j++ {
                twoDimension[i][j] = i + j
        }
}
// => 2d:  [[0 1 2] [1 2 3]]
fmt.Println("2d: ", twoDimension)
```

### 指针

```go
func main () {
    b := *getPointer()
    fmt.Println("值是", b)
}
```

```go
func getPointer () (myPointer *int) {
    a := 234
    return &a
}
```

```go
a := new(int)
*a = 234
```

参见：[指针](https://tour.go.dev/moretypes/1)

### 切片

```go
s := make([]string, 3)
s[0] = "a"
s[1] = "b"
s = append(s, "d")
s = append(s, "e", "f")

fmt.Println(s)
fmt.Println(s[1])
fmt.Println(len(s))
fmt.Println(s[1:3])

slice := []int{2, 3, 4}
```

另见：[切片示例](https://gobyexample.com/slices)

### 常量

```go
const s string = "常量"
const Phi = 1.618
const n = 500000000
const d = 3e20 / n
fmt.Println(d)
```

### 类型转换

```go
i := 90
f := float64(i)
u := uint(i)

// 将等于字符 Z
s := string(i)
```

#### 如何获取整数的字符串表示？

```go
i := 90

// 需要导入 "strconv"
s := strconv.Itoa(i)
fmt.Println(s) // 输出：90
```

## Go 字符串

### 字符串函数

```go
package main

import (
    "fmt"
    s "strings"
)

func main() {
        /* 需要将 strings 导入为 s */
    fmt.Println(s.Contains("test", "e"))

        /* 内建函数 */
        fmt.Println(len("hello"))  // => 5
        // 输出：101
    fmt.Println("hello"[1])
        // 输出：e
    fmt.Println(string("hello"[1]))

}
```

### fmt.Printf {.row-span-2 .col-span-2}

```go
package main

import (
    "fmt"
    "os"
)

type point struct {
    x, y int
}

func main() {
    p := point{1, 2}
    fmt.Printf("%v\n", p)                        // => {1 2}
    fmt.Printf("%+v\n", p)                       // => {x:1 y:2}
    fmt.Printf("%#v\n", p)                       // => main.point{x:1, y:2}
    fmt.Printf("%T\n", p)                        // => main.point
    fmt.Printf("%t\n", true)                     // => true
    fmt.Printf("%d\n", 123)                      // => 123
    fmt.Printf("%b\n", 14)                       // => 1110
    fmt.Printf("%c\n", 33)                       // => !
    fmt.Printf("%x\n", 456)                      // => 1c8
    fmt.Printf("%f\n", 78.9)                     // => 78.9
    fmt.Printf("%e\n", 123400000.0)              // => 1.234e+08
    fmt.Printf("%E\n", 123400000.0)              // => 1.234E+08
    fmt.Printf("%s\n", "\"string\"")             // => "string"
    fmt.Printf("%q\n", "\"string\"")             // => "\"string\""
    fmt.Printf("%x\n", "hex this")               // => 6865782074686973
    fmt.Printf("%p\n", &p)                       // => 0xc00002c040 (地址可能不同)
    fmt.Printf("|%6d|%6d|\n", 12, 345)           // => |    12|   345|
    fmt.Printf("|%6.2f|%6.2f|\n", 1.2, 3.45)     // => |  1.20|  3.45|
    fmt.Printf("|%-6.2f|%-6.2f|\n", 1.2, 3.45)   // => |1.20  |3.45  |
    fmt.Printf("|%6s|%6s|\n", "foo", "b")        // => |   foo|     b|
    fmt.Printf("|%-6s|%-6s|\n", "foo", "b")      // => |foo   |b     |

    s := fmt.Sprintf("a %s", "string")
    fmt.Println(s)

    fmt.Fprintf(os.Stderr, "an %s\n", "error")
}

```

另见：[fmt](https://go.dev/pkg/fmt/)

### 函数示例

| 示例                          | 结果        |
| ----------------------------- | ----------- |
| Contains("test", "es")        | true        |
| Count("test", "t")            | 2           |
| HasPrefix("test", "te")       | true        |
| HasSuffix("test", "st")       | true        |
| Index("test", "e")            | 1           |
| Join([]string{"a", "b"}, "-") | a-b         |
| Repeat("a", 5)                | aaaaa       |
| Replace("foo", "o", "0", -1)  | f00         |
| Replace("foo", "o", "0", 1)   | f0o         |
| Split("a-b-c-d-e", "-")       | [a b c d e] |
| ToLower("TEST")               | test        |
| ToUpper("test")               | TEST        |

## Go 流程控制

### 条件语句

```go

a := 10

if a > 20 {
        fmt.Println(">")
} else if a < 20 {
        fmt.Println("<")
} else {
        fmt.Println("=")
}
```

### if 中的语句

```go
x := "你好 go！"

if count := len(x); count > 0 {
        fmt.Println("是的")
}

```

---

```go

if _, err := doThing(); err != nil {
        fmt.Println("出错了")
}
```

### Switch

```go {.wrap}
x := 42.0
switch x {
case 0:
case 1, 2:
        fmt.Println("多个匹配")
case 42:   // 不会“穿透”。
        fmt.Println("到达")
case 43:
        fmt.Println("未到达")
default:
        fmt.Println("可选")
}
```

参见：[Switch](https://github.com/golang/go/wiki/Switch)

### For 循环

```go
for i := 0; i <= 10; i++ {
    fmt.Println("i: ", i)
}
```

### For-Range 循环

```go {.wrap}
nums := []int{2, 3, 4}
sum := 0
for _, num := range nums {
        sum += num
}
fmt.Println("总和:", sum)
```

### While 循环

```go
i := 1
for i <= 3 {
        fmt.Println(i)
        i++
}
```

### Continue 关键字

```go
for i := 0; i <= 5; i++ {
        if i % 2 == 0 {
                continue
        }
        fmt.Println(i)
}
```

### Break 关键字

```go
for {
        fmt.Println("循环")
        break
}
```

## Go 结构体和映射

### 定义 {.row-span-2}

```go
package main

import (
    "fmt"
)

type Vertex struct {
    X int
    Y int
}

func main() {
    v := Vertex{1, 2}
    v.X = 4
    fmt.Println(v.X, v.Y) // => 4 2
}
```

参见：[结构体](https://tour.go.dev/moretypes/2)

### 字面量

```go
v := Vertex{X: 1, Y: 2}
// 字段名可以省略
v := Vertex{1, 2}
// Y 是隐式的
v := Vertex{X: 1}
```

你也可以写上字段名。

### 映射 {.row-span-2}

```go
m := make(map[string]int)
m["k1"] = 7
m["k2"] = 13
fmt.Println(m) // => map[k1:7 k2:13]

v1 := m["k1"]
fmt.Println(v1)     // => 7
fmt.Println(len(m)) // => 2

delete(m, "k2")
fmt.Println(m) // => map[k1:7]

_, prs := m["k2"]
fmt.Println(prs) // => false

n := map[string]int{"foo": 1, "bar": 2}
fmt.Println(n) // => map[bar:2 foo:1] (顺序可能不同)
```

### 指向结构体的指针

```go
v := &Vertex{1, 2}
v.X = 2
```

当 `v` 是一个指针时，`v.X` 等同于 `(*v).X`。

## Go 函数

### 多个参数

```go
func plus(a int, b int) int {
        return a + b
}
func plusPlus(a, b, c int) int {
        return a + b + c
}
fmt.Println(plus(1, 2))
fmt.Println(plusPlus(1, 2, 3))
```

### 多个返回值

```go
func vals() (int, int) {
        return 3, 7
}

a, b := vals()
fmt.Println(a)    // => 3
fmt.Println(b)    // => 7
```

### 函数字面量

```go
r1, r2 := func() (string, string) {
        x := []string{"你好", "速查表.zip"}
        return x[0], x[1]
}()

// => 你好 速查表.zip
fmt.Println(r1, r2)
```

### 裸返回

```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}

x, y := split(17)
fmt.Println(x)   // => 7
fmt.Println(y)   // => 10
```

注意，使用裸返回会降低可读性。

### 可变参数函数

```go
func sum(nums ...int) {
        fmt.Print(nums, " ")
        total := 0
        for _, num := range nums {
                total += num
        }
        fmt.Println(total)
}
sum(1, 2)     //=> [1 2] 3
sum(1, 2, 3)  // => [1 2 3] 6

nums := []int{1, 2, 3, 4}
sum(nums...)  // => [1 2 3 4] 10
```

### init 函数

```go
import --> const --> var --> init()
```

---

```go
var num = setNumber()

func setNumber() int {
        return 42
}
func init() {
        num = 0
}
func main() {
        fmt.Println(num) // => 0
}
```

### 函数作为值

```go
func main() {
        // 将函数赋值给一个名称
        add := func(a, b int) int {
                return a + b
        }
        // 使用名称调用函数
        fmt.Println(add(3, 4)) // => 7
}
```

### 闭包 1

```go
func scope() func() int{
        outer_var := 2
        foo := func() int {return outer_var}
        return foo
}

// 输出：2
fmt.Println(scope()())
```

### 闭包 2

```go
func outer() (func() int, int) {
        outer_var := 2
        inner := func() int {
                outer_var += 99
                return outer_var
        }
        inner()
        return inner, outer_var
}
inner, val := outer()
fmt.Println(inner()) // => 200
fmt.Println(val)     // => 101
```

## Go 包

### 导入 {.row-span-2}

```go
import "fmt"
import "math/rand"
```

#### 等同于

```go
import (
    "fmt"        // 提供 fmt.Println
    "math/rand"  // 提供 rand.Intn
)
```

参见：[导入](https://tour.go.dev/basics/1)

### 别名 {.row-span-2}

```go
import r "math/rand"
```

---

```go
import (
        "fmt"
        r "math/rand"
)
```

---

```go
r.Intn()
```

### 包

```go
package main

// 内部包只能被位于 internal 目录父目录下的
// 另一个包导入
package internal
```

参见：[内部包](https://go.dev/doc/go1.4#internalpackages)

### 导出名称

```go
// 以大写字母开头
func Hello () {
    ···
}
```

参见：[导出名称](https://tour.go.dev/basics/3)

## Go 并发

### Goroutines {.row-span-2}

```go
package main

import (
    "fmt"
    "time"
)

func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

func main() {
    f("直接")
    go f("goroutine")

    go func(msg string) {
        fmt.Println(msg)
    }("进行中")

    time.Sleep(time.Second)
    fmt.Println("完成")
}
```

参见：[Goroutines](https://tour.go.dev/concurrency/1)，[通道](https://tour.go.dev/concurrency/2)

### WaitGroup {.row-span-2}

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

func w(id int, wg *sync.WaitGroup) {
    defer wg.Done()
    fmt.Printf("%d 开始\n", id)

    time.Sleep(time.Second)
    fmt.Printf("%d 完成\n", id)
}

func main() {
    var wg sync.WaitGroup
    for i := 1; i <= 5; i++ {
        wg.Add(1)
        go w(i, &wg)
    }
    wg.Wait()
}
```

参见：[WaitGroup](https://go.dev/pkg/sync/#WaitGroup)

### 关闭通道

```go
ch <- 1
ch <- 2
ch <- 3
close(ch) // 关闭一个通道
```

---

```go
// 迭代通道直到关闭
for i := range ch {
    ···
}
```

---

```go
// 如果 `ok == false` 则表示已关闭
v, ok := <- ch
```

参见：[Range 和 close](https://tour.go.dev/concurrency/4)

### 带缓冲的通道

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
ch <- 3
// 致命错误：
// 所有 goroutine 都已休眠 - 死锁
```

参见：[带缓冲的通道](https://tour.go.dev/concurrency/3)

## Go 错误控制

### Deferring 函数

```go
func main() {
    defer func() {
        fmt.Println("完成")
    }()
    fmt.Println("工作中...")
}
```

### Lambda defer

```go
func main() {
    var d = int64(0)
    defer func(d *int64) {
        fmt.Printf("& %v Unix 秒\n", *d)
    }(&d)
    fmt.Print("完成 ")
    d = time.Now().Unix()
}
```

defer 函数使用 d 的当前值，除非我们使用指针在 main 结束时获取最终值。

### Defer

```go
func main() {
    defer fmt.Println("完成")
    fmt.Println("工作中...")
}
```

参见：[Defer, panic 和 recover](https://blog.go.dev/defer-panic-and-recover)

## Go 方法 {.cols-2}

### 接收者

```go
type Vertex struct {
    X, Y float64
}
```

```go
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X * v.X + v.Y * v.Y)
}
```

```go
v := Vertex{1, 2}
v.Abs()
```

参见：[方法](https://tour.go.dev/methods/1)

### 修改

```go
func (v *Vertex) Scale(f float64) {
    v.X = v.X * f
    v.Y = v.Y * f
}
```

```go
v := Vertex{6, 12}
v.Scale(0.5)
// `v` 被更新
```

参见：[指针接收者](https://tour.go.dev/methods/4)

## Go 接口 {.cols-2}

### 一个基本接口

```go
type Shape interface {
    Area() float64
    Perimeter() float64
}
```

### 结构体

```go
type Rectangle struct {
    Length, Width float64
}
```

结构体 `Rectangle` 通过实现 `Shape` 接口的所有方法来隐式实现该接口。

### 方法

```go
func (r Rectangle) Area() float64 {
    return r.Length * r.Width
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.Length + r.Width)
}
```

`Shape` 中定义的方法在 `Rectangle` 中实现。

### 接口示例

```go {.wrap}
func main() {
    var r Shape = Rectangle{Length: 3, Width: 4}
    fmt.Printf("r 的类型：%T，面积：%v，周长：%v。", r, r.Area(), r.Perimeter())
}

```

## Go 泛型 {.cols-2}

### 示例 1

```go
// comparable 表示可以比较的类型。
type comparable interface {
    int | float64 | string
}

// Max 返回两个可比较值中的最大值。
func Max[T comparable](a, b T) T {
    if a > b {
        return a
    }
    return b
}

func main() {
    // 查找两个整数中的最大值。
    maxInt := Max(10, 20)
    fmt.Println("最大整数：", maxInt)

    // 查找两个浮点数中的最大值。
    maxFloat := Max(3.14, 2.71)
    fmt.Println("最大浮点数：", maxFloat)

    // 查找两个字符串中的最大值。
    maxString := Max("apple", "banana")
    fmt.Println("最大字符串：", maxString)
}

```

### 示例 2

```go

// Pair[T, U] 表示一个泛型的值对。
type Pair[T, U any] struct {
    First  T
    Second U
}

func main() {
    pair := Pair[int, string]{First: 42, Second: "hello"}

    fmt.Println("第一个值：", pair.First)
    fmt.Println("第二个值：", pair.Second)

    // 打印值对中值的类型。
    fmt.Println("第一个值的类型：", reflect.TypeOf(pair.First))
    fmt.Println("第二个值的类型：", reflect.TypeOf(pair.Second))
}

```

## Go 文件 I/O {.cols-2}

### 读取文件
将文件内容读入内存。
```go
data, err := os.ReadFile("file.txt")
if err != nil {
        log.Fatal(err)
}
```

### 写入文件
将数据写入文件，并指定权限（例如，0644 表示读写）。
```go
err := os.WriteFile("file.txt", []byte("你好，Go！"), 0644)
```

## Go 测试 {.cols-2}

### 单元测试
单元测试：一个基本的单元测试遵循以下命名约定，并使用 t.Errorf() 报告失败。
```go
func TestAdd(t *testing.T) {
        result := add(2, 3)
        if result != 5 {
                t.Errorf("期望得到 5，实际得到 %d", result)
        }
}
```

### 基准测试
基准测试：基准测试衡量性能，使用 b.N 控制迭代次数。
```go
func BenchmarkAdd(b *testing.B) {
        for i := 0; i < b.N; i++ {
                add(1, 2)
        }
}
```

## Go JSON 处理 {.cols-2}


### JSON 编码
将 Go 结构体转换为 JSON。
```go
data, _ := json.Marshal(person)
```

### JSON 解码
将 JSON 数据解析到 Go 结构体中。
```go
json.Unmarshal(data, &person)
```

## Go 服务器 {.cols-2}

### net/http (标准库)
```go
package main

import (
        "fmt"
        "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
        fmt.Fprint(w, "来自 net/http 的问候！")
}

func main() {

        http.HandleFunc("/", handler)

        http.ListenAndServe(":8080", nil)
}

```

### gorilla/mux
```go
package main

import (
        "fmt"
        "net/http"
        "github.com/gorilla/mux"
)

func main() {

        r := mux.NewRouter()

        r.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprint(w, "来自 Gorilla Mux 的问候！")
        })

        http.ListenAndServe(":8081", r)
}

```

### chi
```go
package main

import (
        "fmt"
        "net/http"
        "github.com/go-chi/chi/v5"
)

func main() {

        r := chi.NewRouter()

        r.Get("/", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprint(w, "来自 Chi 的问候！")
        })

        http.ListenAndServe(":8082", r)
}
```

### gin
```go
package main

import (
        "github.com/gin-gonic/gin"
)

func main() {

        r := gin.Default()

        r.GET("/", func(c *gin.Context) {
                c.String(200, "来自 Gin 的问候！")
        })

        r.Run(":8083")
}
```

### fiber
```go
package main

import (
        "github.com/gofiber/fiber/v3"
)

func main() {

        app := fiber.New()

        app.Get("/", func(c *fiber.Ctx) error {
                return c.SendString("来自 Fiber 的问候！")
        })

        app.Listen(":8084")
}
```
### beego
```go
package main

import (
        "github.com/beego/beego/v2/server/web"
)

func main() {

        web.Get("/", func(ctx *web.Context) {
                ctx.Output.Body([]byte("来自 Beego 的问候！"))
        })

        web.Run()
}

```

## 其他

### 关键字

- `break`
- `default`
- `func`
- `interface`
- `select`
- `case`
- `defer`
- `go`
- `map`
- `struct`
- `chan`
- `else`
- `goto`
- `package`
- `switch`
- `const`
- `fallthrough`
- `if`
- `range`
- `type`
- `continue`
- `for`
- `import`
- `return`
- `var`
- `iota`

{.cols-3 .marker-none}

### 运算符和标点符号

|                 |                 |                  |                  |                   |      |       |     |     |
| --------------- | --------------- | ---------------- | ---------------- | ----------------- | ---- | ----- | --- | --- |
| `+`             | `&`             | `+=`             | `&=`             | `&&`              | `==` | `!=`  | `(` | `)` |
| `-`             | <code>\|</code> | `-=`             | <code>\|=</code> | <code>\|\|</code> | `<`  | `<=`  | `[` | `]` |
| <code>\*</code> | `^`             | <code>\*=</code> | `^=`             | `<-`              | `>`  | `>=`  | `{` | `}` |
| `/`             | `<<`            | `/=`             | `<<=`            | `++`              | `=`  | `:=`  | `,` | `;` |
| `%`             | `>>`            | `%=`             | `>>=`            | `--`              | `!`  | `...` | `.` | `:` |
|                 | `&^`            | `&^=`            |                  |                   |      |       |     |     |

## 另请参阅 {.cols-1}

- [Devhints](https://devhints.io/go) _(devhints.io)_
- [Go 语言之旅](https://tour.go.dev/welcome/1) _(tour.go.dev)_
- [Go wiki](https://github.com/golang/go/wiki/) _(github.com)_
- [Effective Go](https://go.dev/doc/effective_go) _(go.dev)_
- [Go 实例教程](https://gobyexample.com/) _(gobyexample.com)_
- [Awesome Go](https://awesome-go.com/) _(awesome-go.com)_
- [JustForFunc Youtube](https://www.youtube.com/channel/UC_BzFbxG2za3bp5NRRRXJSw) _(youtube.com)_
- [代码风格指南](https://github.com/golang/go/wiki/CodeReviewComments) _(github.com)_

