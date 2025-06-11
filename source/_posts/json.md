---
title: JSON
date: 2021-09-14 18:26:55
background: bg-[#646464]
tags:
  - config
  - format
categories:
  - Programming
intro: |
  这是一个用于理解和编写 JSON 格式配置文件的快速参考备忘单。
plugins:
  - copyCode
---

## 入门

### 简介

[JSON](https://json.org/) 是一种轻量级的基于文本的开放标准，专为人类可读的数据交换而设计。

- JSON 代表 JavaScript Object Notation
- JSON 易于阅读和编写。
- JSON 是一种与语言无关的数据交换格式
- JSON 文件扩展名是 `.json`
- JSON 互联网媒体类型是 `application/json`

{.marker-round}

### 示例

```json
{
  "name": "Jason",
  "age": 39,
  "height": 1.92,
  "gender": "M",
  "salary": 70000,
  "married": true,
  "children": [
    { "name": "Tom", "age": 9, "gender": "M" },
    { "name": "Ava", "age": 7, "gender": "F" }
  ]
}
```

### 类型

| 类型      | 描述                             |
| --------- | :-------------------------------------- |
| `Number`  | 双精度浮点数         |
| `String`  | 字符序列                    |
| `Boolean` | `true` 或 `false`                       |
| `Array`   | 值的有序序列              |
| `Value`   | 字符串、数字、布尔值、null 等       |
| `Object`  | 键/值对的无序集合 |
| `null`    | Null 或空                           |

### 字符串 {.row-span-3}

|      |                            |
| ---- | :------------------------- |
| `\"` | 双引号               |
| `\\` | 反斜杠                  |
| `\/` | 正斜杠              |
| `\b` | 退格                  |
| `\f` | 换页符                  |
| `\n` | 换行符                    |
| `\r` | 回车符            |
| `\t` | 制表符                        |
| `\u` | 后跟四个十六进制数字 |

#### 示例

```json {.wrap}
{
  "url": "https://r3f.cn",
  "msg": "Hi,\n\"r3f.cn\"",
  "intro": "Share quick reference and cheat sheet for developers."
}
```

#### 无效字符串

```json
{ "foo": "bar" }
```

必须用双引号分隔

### 数字 {.row-span-2}

| 类型       | 描述                            |
| ---------- | :------------------------------------- |
| `Integer`  | 数字 1-9、0 以及正数或负数 |
| `Fraction` | 小数，如 0.3、3.9                |
| `Exponent` | 指数，如 e、e+、e-、E、E+、E      |

#### 示例

```json
{
  "positive": 12,
  "negative": -1,
  "fraction": 10.25,
  "exponent": 1.0e2,
  "zero": 0
}
```

#### 无效数字

```json
{ "foo": 0xff }
```

在 JSON 中，您只能使用十进制字面量

### 对象

```json
{
  "color": "Purple",
  "id": "210",
  "composition": {
    "R": 70,
    "G": 39,
    "B": 89
  },
  "empty_object": {}
}
```

多个键/值对，用逗号分隔

### 数组

```json
[1, 2, 3, 4, 5]
```

以 `[` 开始，以 `]` 结束

### 对象数组

```json
{
  "children": [
    { "name": "Jimmy Smith", "age": 15 },
    { "name": "Sammy Sosa", "age": 12 }
  ]
}
```

### 数组对象

```json
{
  "attributes": ["a1", "a2"],
  "methods": ["getter", "setter"],
  "empty_array": []
}
```

### 二维数组

```json
{
  "my_sequences": [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9, 0],
    [10, 11]
  ]
}
```

### 对象嵌套对象

```json
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

### 嵌套

```json
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

## 在 JavaScript 中访问 JSON

### 访问对象

```javascript
let myObject = {
  name: "Jason",
  last: "Doe",
  age: 39,
  gender: "M",
  salary: 70000,
  married: true,
};
```

---

|                    |           |
| ------------------ | :-------- |
| `myObject.name`    | "Jason"   |
| `myObject["name"]` | "Jason"   |
| `myObject.age`     | 39        |
| `myObject.other`   | undefined |
| `myObject[0]`      | undefined |

### 访问嵌套对象 {.row-span-2}

```javascript
let myObject = {
  ref: {
    name: 0,
    last: 1,
    age: 2,
    gender: 3,
    salary: 4,
    married: 5,
  },
  jdoe: ["Jason", "Doe", 39, "M", 70000, true],
  jsmith: ["Tom", "Smith", 42, "F", 80000, true],
};
```

---

|                          |                          |
| ------------------------ | :----------------------- |
| `myObject.ref.age`       | 2                        |
| `myObject["ref"]["age"]` | 2                        |
| `myObject.jdoe`          | ["Jason", "Doe", 39 ...] |
| `myObject.jsmith[3]`     | "F"                      |
| `myObject[1]`            | undefined                |

### 访问对象数组 {.row-span-2}

```javascript
let myArray = [
  {
    name: "Jason",
    last: "Doe",
    age: 39,
    gender: "M",
    salary: 70000,
    married: true,
  },
  {
    name: "Tom",
    last: "Smith",
    age: 42,
    gender: "F",
    salary: 80000,
    married: true,
  },
  {
    name: "Amy",
    last: "Burnquist",
    age: 29,
    gender: "F",
    salary: 60000,
    married: false,
  },
];
```

---

|                     |                            |
| ------------------- | :------------------------- |
| `myArray[0]`        | `{`"name": "Jason", ...`}` |
| `myArray[1].name`   | "Tom"                      |
| `myArray[1][2]`     | 42                         |
| `myArray[3]`        | undefined                  |
| `myArray[3].gender` | TypeError: Cannot read...  |

### 访问数组

```javascript
let myArray = ["Jason", "Doe", 39, "M", 70000, true];
```

---

|              |           |
| ------------ | :-------- |
| `myArray[1]` | "Doe"     |
| `myArray[5]` | true      |
| `myArray[6]` | undefined |

## 另请参阅 {.cols-1}

- [JSON](https://www.json.org/json-en.html) _(json.org)_
- [JSON Editor Online](http://jsoneditoronline.org/) _(jsoneditoronline.org)_
- [Convert JSON Array to Markdown Table, CSV and more](https://tableconvert.com/json-to-markdown) _(tableconvert.com)_

