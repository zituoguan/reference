---
title: TOML 格式参考
date: 2020-12-29 20:36:35
background: bg-[#848484]
tags:
  - config
  - format
categories:
  - 编程
intro: |
  这是一份 TOML 格式配置文件语法的快速参考备忘单。
plugins:
  - copyCode
---

## 入门指南

### 简介

[TOML](https://toml.io/en/) 是一种极简的配置文件格式，因其显而易见的语义而易于阅读。

- [文档](https://toml.io/en/latest) _(toml.io)_
- [X分钟学习Y](https://learnxinyminutes.com/docs/toml/) _(learnxinyminutes.com)_

### 示例

```toml
bool = true
date = 2006-05-27T07:32:00Z
string = "hello"
number = 42
float = 3.14
scientificNotation = 1e+12
```

### 注释

```yaml
# 单行注释示例

# 块级注释示例
# 注释行 1
# 注释行 2
# 注释行 3
```

### 整数 (Integer)

```toml
int1 = +42
int2 = 0
int3 = -21
integerRange = 64
```

### 浮点数 (Float)

```toml
float2 = 3.1415
float4 = 5e+22
float7 = 6.626e-34
```

### 布尔值 (Boolean)

```toml
bool1 = true
bool2 = false
boolMustBeLowercase = true
```

### 日期时间 (Datetime)

```toml
date1 = 1989-05-27T07:32:00Z
date2 = 1989-05-26T15:32:00-07:00
date3 = 1989-05-27T07:32:00
date4 = 1989-05-27
time1 = 07:32:00
time2 = 00:32:00.999999
```

### 字符串 (String)

```toml
str1 = "I'm a string."
str2 = "You can \"quote\" me."
str3 = "Name\tJos\u00E9\nLoc\tSF."
```

参见: [字符串](#toml-strings)

### 表 (Table)

```toml
[owner]
name = "Tom Preston-Werner"
dob = 1979-05-27T07:32:00-08:00
```

参见: [表](#toml-tables)

### 数组 (Array)

```toml
array1 = [1, 2, 3]
array2 = ["Commas", "are", "delimiter"]
array3 = [8001, 8001, 8002]
```

### 友好数组 (Friendly Array) {.col-span-2}

```toml
array1 = [ "不要混合", "不同的", "类型" ]
array2 = [ [ 1.2, 2.4 ], ["所有", '字符串', """都是相同的""", '''类型'''] ]
array3 = [
  "空白", "会被",
  "忽略"
]
```

## TOML 字符串

### 多行字符串 (Multiline String)

```toml
multiLineString = """
多行基本字符串由
每侧三个引号包围
并允许换行。
"""
```

### 字面量字符串 (Literal String)

```toml {.wrap}
path = 'C:\Users\nodejs\templates'
path2 = '\\User\admin$\system32'
quoted = 'Tom "Dubs" Preston-Werner'
regex = '<\i\c*\s*>'
```

由单引号包围。不允许转义。

### 多行字面量字符串 (MultiLine Literal String)

```toml
re = '''\d{2} apps is t[wo]o many'''
lines = '''
原始字符串中的第一个换行符
会被修剪掉。
所有其他空白
都会被保留。
'''
```

## TOML 表

### 基本表 (Basic)

```toml
[name]
foo = 1
bar = 2
```

`foo` 和 `bar` 是名为 `name` 的表中的键。

### 嵌套表 (Nested)

```toml
[table1]
  foo = "bar"

[table1.nested_table]
  baz = "bat"
```

### 数组型表 (Array-like) {.row-span-2}

```toml
[[comments]]
author = "Nate"
text = "很棒的文章！"

[[comments]]
author = "Anonymous"
text = "喜欢！"
```

#### ↓ 等效 JSON

```json
{
  "comments": [
    {
      "author": "Nate",
      "text": "很棒的文章！"
    },
    {
      "author": "Anonymous",
      "text": "喜欢！"
    }
  ]
}
```

### 点分隔表名 (Dot separated)

```toml
[dog."tater.man"]
type = "pug"
```

#### ↓ 等效 JSON

```json
{
  "dog": {
    "tater.man": {
      "type": "pug"
    }
  }
}
```

### 多层嵌套表 (Multi-nested)

```toml
[foo.bar.baz]
bat = "hi"
```

#### ↓ 等效 JSON

```json
{
  "foo": {
    "bar": {
      "baz": {
        "bat": "hi"
      }
    }
  }
}
```

### 忽略空白 (Ignore whitespace)

```toml
[a.b.c]          # 这是最佳实践
[ d.e.f ]        # 等同于 [d.e.f]
[ g .  h  .i ]   # 等同于 [g.h.i]
[ j . "ʞ" .'l' ] # 等同于 [j."ʞ".'l']
```

### 内联表 (Inline Table) {.col-span-2}

```toml
name = { first = "Tom", last = "Preston-Werner" }
point = { x = 1, y = 2 }
animal = { type.name = "pug" }
```
