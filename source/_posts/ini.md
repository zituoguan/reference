---
title: INI
date: 2022-12-30 09:51:44
background: bg-[#6d94c7]
tags:
categories:
  - 编程
intro: |
  这是一个用于理解和编写 INI 格式配置文件的快速参考备忘单。
plugins:
  - copyCode
---

## 入门

### 简介

- INI 是一种具有固定标准格式的配置文件
- 基本元素是键或属性
- 每个键由一个**名称**和一个**值**组成，用等号 (`=`) 分隔
- **键名**显示在等号的**左侧**
- 等号 (`=`) 和分号 (`;`) 是**保留**字符
- INI 配置方法源于 MS-DOS 操作系统

现在作为许多配置的非正式标准，其他操作系统可能使用 `.conf` 或 `.cfg` 作为后缀

### 示例

```ini
; 这是注释
[owner]
name=张三
organization=Acme 产品

[database]
; 这是注释
server=192.0.2.42
port=143
file="acme payroll.dat"

[section.subsection]
foo = bar
```

### 注释

注释 (`;`)

```ini
; 这是注释文本，将被忽略
```

注释 (`#`)

```ini
# 这是注释文本，⚠️ 一些编译器支持它
```

行后注释 (`;`,`#`) _(非标准)_

```ini
var = a ; 这是一个行内注释
foo = bar # 这是另一个行内注释
```

在某些情况下，注释必须单独占一行

### 节

- 名称单独占一行
- 名称用方括号 `[` 和 `]` 括起来
- 没有显式的 `节结束` 分隔符
- 在下一个 `节` 声明处或文件末尾结束
- 节和属性名称不区分大小写
<!--rehype:className=style-round-->

```ini
[section]
key1 = a
key2 = b
```

与下面的 `JSON` 相同 👇

```json
{
  "section": {
    "key1": "a",
    "key2": "b"
  }
}
```

### 嵌套 (某些解析器支持)

```ini
[section]
domain = r3f.cn
[section.subsection]
foo = bar
```

与下面的 `JSON` 相同 👇

```json
{
  "section": {
    "domain": "r3f.cn",
    "subsection": {
      "foo": "bar"
    }
  }
}
```

嵌套到上一节 (简写)

```ini
[section]
domain = r3f.cn
[.subsection]
foo = bar
```

### 转义字符

| 序列     | 含义                                                                                             |
| :------- | :----------------------------------------------------------------------------------------------- |
| `\\`     | \ (单个反斜杠，转义转义字符)                                                                       |
| `\'`     | 撇号                                                                                             |
| `\"`     | 双引号                                                                                           |
| `\0`     | 空字符                                                                                           |
| `\a`     | 响铃/警报/声音                                                                                   |
| `\b`     | 退格，对于某些应用程序是 [响铃字符] (https://en.wikipedia.org/wiki/Bell_character)                 |
| `\t`     | 制表符                                                                                           |
| `\r`     | 回车符                                                                                           |
| `\n`     | 换行符                                                                                           |
| `\;`     | 分号                                                                                             |
| `\#`     | 井号                                                                                             |
| `\=`     | 等号                                                                                             |
| `\:`     | 冒号                                                                                             |
| `\x????` | 对应于 ???? 的十六进制代码点的 Unicode 字符                                                        |

### 数组

```ini
[section]
domain = r3f.cn
array[]=第一个值
array[]=第二个值
```

与下面的 `JSON` 相同 👇

```json
{
  "section": {
    "domain": "r3f.cn",
    "array": ["第一个值", "第二个值"]
  }
}
```

### 解析器

- [@go-ini/ini](https://github.com/go-ini/ini) _(golang)_
- [@npm/ini](https://www.npmjs.com/package/ini) _(nodejs)_
- [@zonyitoo/rust-ini](https://github.com/zonyitoo/rust-inii) _(rust)_
- [@rxi/ini](https://www.npmjs.com/package/ini) _(c)_
- [@pulzed/mINI](https://github.com/pulzed/mINI) _(c++)_
- [@rickyah/ini-parser](https://github.com/rickyah/ini-parser) _(c#)_
- [@Enichan/Ini](https://github.com/Enichan/Ini) _(c#)_

## 另请参阅

- [INI 文件配置](https://zh.wikipedia.org/wiki/INI%E6%96%87%E4%BB%B6)_(wikipedia.org)_
