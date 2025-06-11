---
title: YAML
date: 2020-12-29 18:26:55
background: bg-[#b42e28]
tags:
  - config
  - format
categories:
  - 编程
intro: |
  这是一个用于理解和编写 YAML 格式配置文件的快速参考备忘单。
plugins:
  - copyCode
---

## 入门

### 简介

[YAML](https://yaml.org/) 是一种数据序列化语言，旨在让人类可以直接编写和阅读。

- YAML 不允许使用制表符
- 元素各部分之间必须有空格
- YAML 区分大小写
- YAML 文件以 `.yaml` 或 `.yml` 扩展名结尾
- YAML 是 JSON 的超集
- Ansible playbooks 是 YAML 文件 {.marker-round}

### 标量类型 {.row-span-2}

<!-- prettier-ignore -->
```yaml
n1: 1            # 整数
n2: 1.234        # 浮点数

s1: 'abc'        # 字符串
s2: "abc"        # 字符串
s3: abc          # 字符串

b: false         # 布尔类型

d: 2015-04-05    # 日期类型
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "n1": 1,
  "n2": 1.234,
  "s1": "abc",
  "s2": "abc",
  "s3": "abc",
  "b": false,
  "d": "2015-04-05"
}
```

使用空格进行缩进。元素各部分之间必须有空格。

### 变量

```yaml
some_thing: &VAR_NAME foobar
other_thing: *VAR_NAME
```

#### ↓ 等效 JSON

<!-- prettier-ignore -->
```json {.wrap}
{
  "some_thing": "foobar",
  "other_thing": "foobar"
}
```

### 注释

```yaml
# 单行注释示例

# 块级注释示例
# 注释行 1
# 注释行 2
# 注释行 3
```

### 多行字符串

```yaml
description: |
  hello
  world
```

#### ↓ 等效 JSON

```json {.wrap}
{ "description": "hello\nworld\n" }
```

### 继承 {.row-span-2}

```yaml
parent: &defaults
  a: 2
  b: 3

child:
  <<: *defaults
  b: 4
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "parent": {
    "a": 2,
    "b": 3
  },
  "child": {
    "a": 2,
    "b": 4
  }
}
```

### 引用 {.row-span-2}

```yaml
values: &ref
  - Will be
  - reused below

other_values:
  i_am_ref: *ref
```

#### ↓ 等效 JSON

<!-- prettier-ignore -->
```json {.wrap}
{
  "values": [
    "Will be",
    "reused below"
  ],
  "other_values": {
    "i_am_ref": [
      "Will be",
      "reused below"
    ]
  }
}
```

### 折叠字符串

```yaml
description: >
  hello world
```

#### ↓ 等效 JSON

```json {.wrap}
{ "description": "hello world\n" }
```

### 两个文档

```yaml
---
document: 这是文档 1
---
document: 这是文档 2
```

YAML 使用 `---` 来分隔指令和文档内容。

## YAML 集合

### 序列

```yaml
- Mark McGwire
- Sammy Sosa
- Ken Griffey
```

#### ↓ 等效 JSON

<!-- prettier-ignore -->
```json {.wrap}
[
  "Mark McGwire",
  "Sammy Sosa",
  "Ken Griffey"
]
```

### 映射

<!-- prettier-ignore -->
```yaml
hr:  65       # 本垒打
avg: 0.278    # 打击率
rbi: 147      # 打点
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "hr": 65,
  "avg": 0.278,
  "rbi": 147
}
```

### 映射到序列

```yaml
attributes:
  - a1
  - a2
methods: [getter, setter]
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "attributes": ["a1", "a2"],
  "methods": ["getter", "setter"]
}
```

### 映射序列

<!-- prettier-ignore -->
```yaml
children:
  - name: Jimmy Smith
    age: 15
  - name: Jimmy Smith
    age: 15
  -
    name: Sammy Sosa
    age: 12
```

#### ↓ 等效 JSON

<!-- prettier-ignore -->
```json {.wrap}
{
  "children": [
    {"name": "Jimmy Smith", "age": 15},
    {"name": "Jimmy Smith", "age": 15},
    {"name": "Sammy Sosa", "age": 12}
  ]
}
```

### 序列的序列

<!-- prettier-ignore -->
```yaml
my_sequences:
  - [1, 2, 3]
  - [4, 5, 6]
  -
    - 7
    - 8
    - 9
    - 0
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "my_sequences": [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9, 0]
  ]
}
```

### 映射的映射

```yaml
Mark McGwire: { hr: 65, avg: 0.278 }
Sammy Sosa: { hr: 63, avg: 0.288 }
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "Mark McGwire": {
    "hr": 65,
    "avg": 0.278
  },
  "Sammy Sosa": {
    "hr": 63,
    "avg": 0.288
  }
}
```

### 嵌套集合

```yaml
Jack:
  id: 1
  name: Franc
  salary: 25000
  hobby:
    - a
    - b
  location: { country: "A", city: "A-A" }
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "Jack": {
    "id": 1,
    "name": "Franc",
    "salary": 25000,
    "hobby": ["a", "b"],
    "location": {
      "country": "A",
      "city": "A-A"
    }
  }
}
```

### 无序集合

```yaml
set1: !!set
  ? one
  ? two
set2: !!set { "one", "two" }
```

#### ↓ 等效 JSON

```json {.wrap}
{
  "set1": { "one": null, "two": null },
  "set2": { "one": null, "two": null }
}
```

集合表示为一个映射，其中每个键都与一个 null 值相关联。

### 有序映射

```yaml
ordered: !!omap
  - Mark McGwire: 65
  - Sammy Sosa: 63
  - Ken Griffy: 58
```

#### ↓ 等效 JSON

<!-- prettier-ignore -->
```json {.wrap}
{
  "ordered": [
    { "Mark McGwire": 65 },
    { "Sammy Sosa": 63 },
    { "Ken Griffy": 58 }
  ]
}
```

## YAML 参考

### 术语

- 序列 (Sequences) 又称数组 (arrays) 或列表 (lists)
- 标量 (Scalars) 又称字符串 (strings) 或数字 (numbers)
- 映射 (Mappings) 又称哈希 (hashes) 或字典 (dictionaries) {.marker-round}

基于 YAML.org [参考卡片](https://yaml.org/refcard.html)。

### 文档指示符

|       |             |
| ----- | ----------- |
| `%`   | 指令指示符  |
| `---` | 文档头      |
| `...` | 文档结束符  |

### 集合指示符 {.row-span-2}

|      |                               |
| ---- | ----------------------------- |
| `?`  | 键指示符                      |
| `:`  | 值指示符                      |
| `-`  | 嵌套序列条目指示符            |
| `,`  | 分隔内联分支条目              |
| `[]` | 包围内联序列分支              |
| `{}` | 包围内联键控分支              |

### 别名指示符

|     |             |
| --- | ----------- |
| `&` | 锚点属性    |
| `*` | 别名指示符  |

### 特殊键

|      |                               |
| ---- | ----------------------------- |
| `=`  | 默认“值”映射键                |
| `<<` | 从另一个映射合并键            |

### 标量指示符

|       |                                   |                                                                 | ----------- |
| ----- | --------------------------------- | --------------------------------------------------------------- | ----------- |
| `''`  | 包围内联未转义标量                |                                                                 |
| `"`   | 包围内联转义标量                  |                                                                 |
| `     | `                                 | 块标量指示符                                                    |
| `>`   | 折叠标量指示符                    |                                                                 |
| `-`   | 去除 chomp 修饰符 (`           | -` 或 `>-`)                                                     |
| `+`   | 保留 chomp 修饰符 (`            | +` 或 `>+`)                                                     |
| `1-9` | 显式缩进修饰符 (`  | 1` 或 `>2`)。 <br/> 修饰符可以组合 (` | 2-`, `>+1`) |

### 标签属性 (通常未指定) {.col-span-2}

|          |                                                             |
| -------- | ----------------------------------------------------------- |
| `none`   | 未指定标签 (由应用程序自动解析)                             |
| `!`      | 非特定标签 (默认为 `!!map`/`!!seq`/`!!str`)                  |
| `!foo`   | 主标签 (按约定，表示本地 `!foo` 标签)                       |
| `!!foo`  | 次要标签 (按约定，表示 `tag:yaml.org,2002:foo`)             |
| `!h!foo` | 需要 `%TAG !h! <prefix>` (然后表示 `<prefix>foo`)           |
| `!<foo>` | 逐字标签 (始终表示 `foo`)                                   |

### 其他指示符

|                  |                      |
| ---------------- | -------------------- |
| `#`              | 注释指示符           |
| <code>\`@</code> | 两者均保留供将来使用 |

### 核心类型 (默认自动标签) {.row-span-2}

|         |                                          |
| ------- | ---------------------------------------- |
| `!!map` | `{哈希表, 字典, 映射}`                   |
| `!!seq` | `{列表, 数组, 元组, 向量, 序列}`         |
| `!!str` | Unicode 字符串                           |

### 转义码 {.row-span-3}

#### 数字

- `\x12` (8位)
- `\u1234` (16位)
- `\U00102030` (32位)

{.cols-2 .marker-none}

#### 保护性

- `\\` (\\)
- `\"` (")
- `\ ` (空格)
- `\<TAB>` (制表符)

{.cols-3 .marker-none}

#### C 语言

- `\0` (NUL 空字符)
- `\a` (BEL 响铃)
- `\b` (BS 退格)
- `\f` (FF 换页)
- `\n` (LF 换行)
- `\r` (CR 回车)
- `\t` (TAB 制表符)
- `\v` (VTAB 垂直制表符)

{.cols-3 .marker-none}

#### 附加

- `\e` (ESC 转义)
- `\_` (NBSP 不换行空格)
- `\N` (NEL 下一行)
- `\L` (LS 行分隔符)
- `\P` (PS 段落分隔符)

{.cols-3 .marker-none}

### 更多类型

|          |                             |
| -------- | --------------------------- |
| `!!set`  | `{樱桃, 李子, 苹果}`        |
| `!!omap` | `[一: 1, 二: 2]`            |

### 语言无关标量类型 {.col-span-2}

|                           |                                            |
| ------------------------- | ------------------------------------------ |
| `{~, null}`               | Null (无值)。                              |
| `[1234, 0x4D2, 02333]`    | [十进制整数, 十六进制整数, 八进制整数]     |
| `[1_230.15, 12.3015e+02]` | [定点浮点数, 指数浮点数]                   |
| `[.inf, -.Inf, .NAN]`     | [无穷大 (浮点数), 负无穷大, 非数字]        |
| `{Y, true, Yes, ON}`      | 布尔真                                     |
| `{n, FALSE, No, off}`     | 布尔假                                     |

## 另请参阅

- [YAML 参考卡片](https://yaml.org/refcard.html) _(yaml.org)_
- [X分钟学习Y](https://learnxinyminutes.com/docs/yaml/) _(learnxinyminutes.com)_
- [YAML 在线校验](http://www.yamllint.com/) _(yamllint.com)_
