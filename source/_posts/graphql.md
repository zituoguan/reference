---
title: GraphQL
date: 2021-07-15 20:51:44
background: bg-[#cc44a2]
tags:
    - 查询
    - API
categories:
    - 编程
intro: |
    本快速参考备忘单简要概述了 GraphQL。
plugins:
    - copyCode
---

## 入门

### 概述

- RESTful API 的一种替代方法
- GraphQL 是一种 API 查询语言
- 使用清晰共享的术语轻松描述 GraphQL API 的结构。
- 客户端发出查询/变更以读取和更新数据
- GraphQL 语法可以表达复杂的实体关系
- 用于在[不同语言](https://graphql.org/code/)中实现 GraphQL 的库

[GraphQL](https://graphql.org/) {.link-arrow}

### Schema (模式)

|                |                                  |
| -------------- | -------------------------------- |
| `schema`       | GraphQL 模式定义                 |
| `query`        | 读取和遍历数据                   |
| `mutation`     | 修改数据或触发操作               |
| `subscription` | 事件发生时运行查询               |

### 内建标量类型

|           |                                              |
| --------- | -------------------------------------------- |
| `Int`     | 有符号 32 位整数                             |
| `Float`   | 有符号双精度浮点值                           |
| `String`  | UTF‐8 字符序列                               |
| `Boolean` | true 或 false                                |
| `ID`      | 唯一标识符                                   |

### 类型定义

|             |                   |
| ----------- | ----------------- |
| `scalar`    | 标量类型          |
| `type`      | 对象类型          |
| `interface` | 接口类型          |
| `union`     | 联合类型          |
| `enum`      | 枚举类型          |
| `input`     | 输入对象类型      |

### 类型修饰符

|              |                                   |
| ------------ | --------------------------------- |
| `String`     | 可为空的字符串                    |
| `String!`    | 非空字符串                        |
| `[String]`   | 可为空字符串的列表                |
| `[String]!`  | 非空的可为空字符串列表            |
| `[String!]!` | 非空的非空字符串列表              |

### 输入参数 {.row-span-2}

#### 基本输入

```js
type Query {
        users(limit: Int): [User]
}
```

#### 带默认值的输入

```js
type Query {
        users(limit: Int = 10): [User]
}
```

#### 带多个参数的输入

```js
type Query {
        users(limit: Int, sort: String): [User]
}
```

#### 带多个参数和默认值的输入

```js {.wrap}
type Query {
        users(limit: Int = 10, sort: String): [User]
}
type Query {
        users(limit: Int, sort: String = "asc"): [User]
}
type Query {
        users(limit: Int = 10, sort: String = "asc"): [User]
}
```

### 输入类型

```js
input ListUsersInput {
        limit: Int
        since_id: ID
}
```

```js
type Mutation {
        users(params: ListUsersInput): [User]!
}
```

### 自定义标量

```js
scalar Url
type User {
        name: String
        homepage: Url
}
```

### 接口 (Interfaces)

```js
interface Foo {
        is_foo: Boolean
}
interface Goo {
        is_goo: Boolean
}
type Bar implements Foo {
        is_foo: Boolean
        is_bar: Boolean
}
type Baz implements Foo, Goo {
        is_foo: Boolean
        is_goo: Boolean
        is_baz: Boolean
}
```

实现一个或多个接口的对象

### 联合 (Unions)

```js
type Foo {
        name: String
}
type Bar {
        is_bar: String
}
union SingleUnion = Foo
union MultipleUnion = Foo | Bar
type Root {
        single: SingleUnion
        multiple: MultipleUnion
}
```

一个或多个对象的联合

### 枚举 (Enums)

```js {.wrap}
enum USER_STATE {
        NOT_FOUND
        ACTIVE
        INACTIVE
        SUSPENDED
}
type Root {
        stateForUser(userID: ID!): USER_STATE!
        users(state: USER_STATE, limit: Int = 10): [User]
}
```

## 另请参阅

- [GraphQL Schema Language Cheat Sheet](https://github.com/sogko/graphql-schema-language-cheat-sheet) _(github.com)_
