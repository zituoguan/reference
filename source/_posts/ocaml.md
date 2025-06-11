---
title: OCaml
date: 2024-08-14 21:12:00
background: bg-[#ec670f]
tags:
  - scientific
  - functional
categories:
  - 编程
intro: |
  [OCaml](https://www.ocaml.org/) 速查表是 OCaml 编程语言的单页参考表。
plugins:
  - copyCode
---

## 入门指南

### hello.ml

```ml
let () =
  let message = "你好，世界！" in (* 将 "Hello, World!" 翻译为 "你好，世界！" *)
  Printf.printf "%s\n" message
```

#### 编译并运行

```bash
$ ocamlc -o hello.byte hello.ml
$ ./hello.byte
```

#### 使用 Dune 构建并运行

```bash
$ dune build hello.exe
$ _build/default/hello.exe

# 你也可以直接运行
$ dune exec ./hello.exe
```

更多信息请参见 [dune](https://dune.build/) 文档。

### 导入模块

使用 opam 安装模块

```bash
$ opam install hex
```

#### 全局打开

```ml
open Hex
```

#### 局部打开

```ml
Hex.of_string "十六进制字符串" (* 将 "hex string" 翻译为 "十六进制字符串" *)

let open Hex in
  of_string "转换为十六进制" (* 将 "to hex" 翻译为 "转换为十六进制" *)
```

### 注释

#### 行注释与块注释

```ml
(* 单行注释 *)

(* 多行注释
* 用于解释
* 复杂的内容 *)

(* 外部注释
   (* 嵌套注释 *)
   外部注释结束 *)
```

#### 文档注释

```ml
val sum : int -> int -> int
(** [sum x y] 返回两个整数 [x] 和 [y] 的和 *)
```

## 数据类型

### 预定义类型

#### Unit 类型

注意：`#` 表示在顶层（toplevel）执行，后面是输出结果

```ml
# ();; (* 相当于 C 语言中的 void *)
- : unit = ()
```

#### 基本类型

```ml
# 5 ;; (* 整数 *)
- : int = 5

# 3.14 ;;  (* 浮点数 *)
- : float = 3.14

# true ;; (* 布尔值 *)
- : bool = true

# false ;;
- : bool = false

# 'a' ;; (* 字符 *)
- : char = 'a'

# "一个字符串" ;; (* 字符串，将 "a string" 翻译为 "一个字符串" *)
- : string = "a string"

# String.to_bytes "你好" ;; (* 字节序列，将 "hello" 翻译为 "你好" *)
- : bytes = Bytes.of_string "hello"

# (3, 5);; (* 元组 *)
- : int * int = (3, 5)

# ref 0;; (* 引用 *)
- : int ref = {contents = 0}
```

#### Option 与 Result 类型

```ml
# Some 42;;
- : int option = Some 42

# Ok 42;;
- : (int, 'a) result = Ok 42

# Error "404";;
- : ('a, int) result = Error 404
```

### 数组与列表

#### 数组

```ml
# [|0; 1; 2; 3|];; (* 创建一个数组 *)
- : int array = [|0; 1; 2; 3|]

# [|'u'; 's'; 'c'|].(1);; (* 数组访问 *)
- char = 's'
```

数组是可变的

```ml
let scores = [|97; 85; 99|];;
- : int array = [|97; 85; 99|]

# scores.(2) <- 89;; (* 更新一个元素 *)
- unit = ()

# scores;;
- : int array = [|97; 85; 89|]
```

#### 列表

```ml
# [1; 2; 3];;
- : int list = [1; 2; 3;]

# ["a"; "字符串"; "列表"];; (* 将 "str" 和 "lst" 翻译为 "字符串" 和 "列表" *)
- : string list = ["a"; "str"; "lst"]
```

列表是不可变的

```ml
# let lst = [1; 2; 3];;
- : int list = [1; 2; 3]

# let new_lst =  0 :: lst;; (* 前置元素到新列表 *)
- : int list = [0; 1; 2; 3]

# new_lst @ [4;5;6];; (* 合并两个列表 *)
- : int list = [0; 1; 2; 3; 4; 5; 6]
```

### 用户自定义类型

#### 记录 (Records)

捆绑相关数据

```ml
type person = {
  name: string;
  age: int
}

# let zeno = {name = "芝诺"; age = 30};; (* 将 "Zeno" 翻译为 "芝诺" *)
val zeno : person = {name = "Zeno"; age = 30}
```

#### 变体 (Variants)

几种不同但相关的类型

```ml
type shape =
  | Circle of float
  | Rectangle of float * float

# let my_shape = Circle 5.0;;
- : shape = Circle 5.
```

#### 类型别名 (Aliases)

为复杂或常用的类型提供有意义的名称

```ml
type point = float * float

# let origin: point = (0.0, 0.0);;
val origin : point = (0., 0.)
```

## 函数

### 函数

#### 单参数

```ml
let add_one x =
  let result = x + 1 in
  result

# add_one 1;;
- : int = 2
```

#### 多参数

```ml
let sum x y =
  let result = x + y in
  result

# sum 1 2;;
- : int = 3
```

#### 元组参数

```ml
let str_concat (x, y) =
  x ^ " " ^ y

# str_concat ("你好", "OCaml") ;; (* 将 "Hello" 翻译为 "你好" *)
- : string = "Hello Ocaml"
```

### 递归函数

#### rec 关键字

所有递归函数都使用 `rec` 关键字

```ml
let rec factorial n =
  if n < 1 then 1 else n * factorial (n - 1)
```

上述实现可能导致栈溢出。

#### 尾递归

利用辅助函数和 `acc` 参数。

```ml
let rec factorial_helper n acc =
  if n = 0 then acc
  else factorial_helper (n - 1) (n * acc)
```

注意最后的调用是递归函数本身。

```ml
let factorial n = factorial_helper n 1
```

### 函数链式调用

#### 应用操作符 (@@)

从右到左读取，第一个操作是 `sum 2 3`

```ml
(* 计算 log(2 + 3) *)
# log @@ float_of_int @@ sum 2 3 ;;
- : float = 1.609...
```

#### 管道操作符 (|>)

```ml
(* 计算 log((x + y)!) *)
# sum 2 3
  |> factorial
  |> float_of_int
  |> log ;;
- : float = 4.787...
```

`|>` 将函数的输出作为下一个函数的输入传递到管道中。

## 控制流

### If 语句

#### If 语句

```ml
let is_pos x =
  if x > 0 then "正数" else "负数" (* 将 "positive" 和 "negative" 翻译为 "正数" 和 "负数" *)
```

#### If else if

```ml
let f x =
  if x > 3 then "大于 3" (* "gt 3" -> "大于 3" *)
  else if x < 3 then "小于 3" (* "lt 3" -> "小于 3" *)
  else "等于 3" (* "eq 3" -> "等于 3" *)
```

####模式匹配

```ml
let is_pos x =
  match x > 0 with
  | true  -> "正数" (* "positive" -> "正数" *)
  | false -> "负数" (* "negative" -> "负数" *)
```

### 循环

#### For 循环

```ml
for i = 1 to 5 do
  print_int i
done
```

#### While 循环

注意需要 `ref` 来使 while 条件最终变为 false。

```ml
let i = ref 0 in
  while !i < 5 do
    print_int !i;
    i := !i + 1
  done
```

### 操作符

#### 比较操作符

```ml
=         (* 等于 *)
<>        (* 不等于 *)
>         (* 大于 *)
<         (* 小于 *)
>=        (* 大于或等于 *)
<=        (* 小于或等于 *)
```

#### 算术操作符

```ml
(* 整数操作符   浮点数操作符 *)
+                 +.  (* 加法 *)
-                 -.  (* 减法 *)
*                 *.  (* 乘法 *)
/                 /.  (* 除法 *)
                  **  (* 幂 *)
```

## 实用工具

### 列表 (List)

#### 搜索与过滤

```ml
# let lst = [1; 2; 3];;
val lst : int list = [1; 2; 3]

# List.filter (fun x -> x mod 2 = 0) lst;;
- : int list = [2]

# List.find (fun x -> x = 4) lst;;
Exception: Not_found (* 异常：未找到 *)

# List.sort compare [2; 1; 3];;
- : int list = [1; 2; 3]
```

#### 应用转换

```ml
(* 遍历列表并应用函数 f *)
List.iter f lst

(* 将函数映射到每个元素 *)
(* 例如：将 lst 中的每个元素 x 加倍 *)
List.map (fun x -> x + x) lst

(* 在元素之间应用操作符 *)
(* 例如：1 + 2 + 3 *)
List.fold_left (+) 0 lst
```

### 关联列表 (Association Lists)

#### 定义与访问

```ml
let scores =
  [("数学", 91); ("哲学", 89); ("统计", 94)] (* "math", "phil", "stats" -> "数学", "哲学", "统计" *)

# List.assoc "统计" scores;; (* "stats" -> "统计" *)
- : int = 94

# List.mem_assoc "数学" scores;; (* "math" -> "数学" *)
- : bool = true
```

#### 分割与合并

```ml
# List.split scores;;
- : string list * int list = (["数学"; "哲学"; "统计"], [91; 89; 94]) (* "math"; "phil"; "stats" -> "数学"; "哲学"; "统计" *)

# List.combine [1;2;3] [4; 5; 6];;
- : (int * int) list = [(1, 4); (2, 5); (3, 6)]
```

关联列表类似于字典或哈希映射。

### 哈希表 (Hash Tables)

哈希表是可变的。

#### 初始化与添加数据

```ml
# let my_htable = Hashtbl.create 3;;
val my_htable : ('_weak1, '_weak2) Hashtbl.t = <abstr>

# Hashtbl.add my_htable "A" "约翰"; (* "John" -> "约翰" *)
  Hashtbl.add my_htable "A" "简"; (* "Jane" -> "简" *)
  Hashtbl.add my_htable "B" "麦克斯";; (* "Max" -> "麦克斯" *)
```

#### 查找数据

```ml
# Hashtbl.find my_htable "A";;
- : string = "简" (* "Jane" -> "简" *)

(* 查找所有 *)
# Hashtbl.find_all my_htable "A";;
- : string list = ["简"; "约翰"] (* "Jane"; "John" -> "简"; "约翰" *)
```

### 映射 (Maps)

映射是不可变的键值关联表。

#### 初始化与添加数据

```ml
(* Map.Make 函子创建自定义映射模块 *)
# module StringMap = Map.Make(String);;

let books =
  StringMap.empty
  |> StringMap.add "沙丘" ("赫伯特", 1965) (* "Dune", "Herbet" -> "沙丘", "赫伯特" *)
  |> StringMap.add "神经漫游者" ("吉布森", 1984) (* "Neuromancer", "Gibson" -> "神经漫游者", "吉布森" *)
```

#### 查找条目

```ml
(* find_opt 返回包装在 option 中的关联值，否则返回 None *)
# StringMap.find_opt "沙丘" books;; (* "Dune" -> "沙丘" *)
- : (string * int) option = Some ("赫伯特", 1965) (* "Herbet" -> "赫伯特" *)

(* find 返回关联值，否则抛出 Not_Found 异常 *)
# StringMap.find "沙丘" books;; (* "Dune" -> "沙丘" *)
- : string * int = ("赫伯特", 1965) (* "Herbet" -> "赫伯特" *)
```

#### 添加与移除条目

创建一个新的映射，因为映射是不可变的。

```ml
let more_books = books
  |> StringMap.add "基地" ("艾萨克·阿西莫夫", 1951) (* "Foundation", "Isaac Asimov" -> "基地", "艾萨克·阿西莫夫" *)

let less_books = books (* 修正：应为 books |> StringMap.remove "Dune" *)
  |> StringMap.remove "沙丘" (* "Dune" -> "沙丘" *)
```

过滤

```ml
let eighties_books =
    StringMap.filter
      (fun _ (_, year) -> year > 1980 && year < 1990) books (* 修正：number 应为 year *)
```

#### 打印数据

```ml
let print_books map =
  StringMap.iter (fun title (author, year) ->
    Printf.printf "书名: %s, 作者: %s, 年份: %d\n" title author year (* "Title", "Author", "Year" -> "书名", "作者", "年份" *)
  ) map

# let () = print_books eighties_books;;
书名: 神经漫游者, 作者: 吉布森, 年份: 1984 (* "Title: Neuromancer, Author: Gibson, Year: 1984" -> "书名: 神经漫游者, 作者: 吉布森, 年份: 1984" *)
```
