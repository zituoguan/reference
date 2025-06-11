---
title: 速查表
date: 2020-11-25 18:28:43
background: bg-gradient-to-l from-green-400 to-blue-500 hover:from-pink-500 hover:to-yellow-500
tags:
  - 指南
  - 参考
categories:
  - 其他
intro:
  这是您可以在 r3f.cn 上使用的魔法语法变体手册，对于贡献者来说这是一个很好的实践。
plugins:
  - copyCode
---

## 入门指南

### 开发设置

- 克隆仓库 [在 Github 上查看](https://github.com/Fechin/reference.git)
  ```shell script {.wrap}
  $ git clone https://github.com/Fechin/reference.git
  ```
- 在项目目录中安装依赖项
  ```shell script
  $ npm install
  ```
- 启动开发服务器 [http://localhost:4000](http://localhost:4000)
  ```shell script
  $ npm run dev
  ```
- 创建或修改 `source/_posts/{name}.md`
- 向我们发送拉取请求然后放松一下 {.marker-timeline}

参考源代码是一个好习惯
[速查表参考](https://github.com/Fechin/reference/blob/main/source/_posts/quickref.md)。

### 目录结构

```yaml
.
├── source
│   ├── _posts   # 速查表源文件
│   │   ├── awk.md
│   │   ├── vim.md # => r3f.cn/vim
│   │   ├── php.md
│   │   ├── css.md # => r3f.cn/css
│   │   ├── ...
│   └── widget   # 小部件文件
│       └── chmod.html
├── public       # 分发文件
├── _config.yml
├── gulpfile.js
├── package.json
├── postcss.config.js
├── tailwind.config.js
└── themes
    └── coo      # 主题文件
```

### 速查表结构 {.row-span-2}

```yaml
.
├── 区域 1   # 标题
│   ├── 卡片 1
│   ├── 卡片 2
│   ├── 卡片 3
│   ├── ...
├── 区域 2
│   ├── 卡片 1
│   │   ├── 段落
│   │   ├── 代码
│   │   ├── <hr/> (即 "---")
│   │   ├── 列表
│   │   │   ├── 段落
│   │   │   └── 代码
│   │   └── 表格
│   │       ├── 段落
│   │       └── 代码
│   ├── 卡片 2
│   ├── 卡片 3
│   └── ...
├── 区域 3
├── 区域 4
└── ...
```

---

- 一张速查表包含多个区域
- 一个区域包含多个卡片
- 一张卡片可以包含代码、表格、列表和段落
- 一个列表可以包含代码和段落
- 一个表格可以包含代码和段落

### 语法变体

- [区域变体](#section-variants)
- [卡片变体](#card-variants)
- [表格变体](#table-variants)
- [列表变体](#list-variants)
- [代码变体](#code-variants)
- [段落变体](#paragraph-variants)
- [卡片示例](#cards-example)

r3f.cn 支持的所有魔法变体

### 创建 source/\_posts/demo.md

```markdown
## 入门指南

### 列表卡片 {.col-span-2}

- 分享快速参考
- 开发人员速查表 ... {.style-timeline}

### 表格卡片

| id  | name    |
| --- | ------- |
| 1   | Roberta |

{.show-header}
```

## 区域变体

### 区域概览 {.secondary}

| -           | -                               |
| ----------- | ------------------------------- |
| `{.cols-1}` | 单列布局               |
| `{.cols-2}` | 双列布局               |
| `{.cols-3}` | 三列布局 _(默认)_ |
| ...         |                                 |
| `{.cols-6}` | 六列布局               |

---

- 区域包含多个卡片
- 使用 {.cols-`n`} 将区域指定为 `n` 列布局
- 点击下面的预览按钮以聚焦该区域

[预览](/quickref#section-variants) {.link-arrow}

### .cols-1

```text
# 单列示例 {.cols-1}
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  1                                  ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  2                                  ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
```

#### ↓ 源代码

```markdown
## 单列示例 {.cols-1}

### 1

### 2
```

[预览](resolutions#lists-of-resolutions) {.link-arrow}

### .cols-2

```text
# 双列示例
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  1              ┆ ┆  2              ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  3              ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
```

#### ↓ 源代码

```markdown
## 双列示例 {.cols-2}

### 1

### 2

### 3
```

[预览](resolutions#getting-started) {.link-arrow}

### .cols-3 (默认)

```text
# 默认
╭┈┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈┈╮
┆  1       ┆ ┆  2       ┆ ┆  3       ┆
╰┈┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈┈╮
┆  4       ┆
╰┈┈┈┈┈┈┈┈┈┈╯
```

#### ↓ 源代码

```markdown
## 默认

### 1

### 2

### 3

### 4
```

## 卡片变体

### 卡片概览 {.secondary}

#### 指定卡片跨越的列数

| -               | -                      |
| --------------- | ---------------------- |
| `{.col-span-2}` | [示例](#col-span-2) |
| `{.col-span-3}` |                        |
| ...             |                        |
| `.col-span-6}`  |                        |

#### 指定卡片跨越的行数 {.text-left}

| -               | -                      |
| --------------- | ---------------------- |
| `{.row-span-2}` | [示例](#row-span-2) |
| `{.row-span-3}` |                        |
| ...             |                        |
| `{.row-span-6}` |                        |

#### 强调卡片 (即 `H3` 区域)

| -              | -                                         |
| -------------- | ----------------------------------------- |
| `{.primary}`   | 红色标题, [示例](#primary-card)      |
| `{.secondary}` | 黄色标题, [示例](#secondary-card) |

一个完整的示例：[卡片示例](#cards-example)

### .col-span-2 {.row-span-2}

#### 第五个卡片跨越两列

```text
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆  1      ┆ ┆  2      ┆ ┆  3      ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  4      ┆ ┆  5                  ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1

### 2

### 3

### 4

### 5 {.col-span-2}
```

#### 第二个卡片跨越两列

```text
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
┆  1      ┆ ┆  2                  ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆  3      ┆ ┆  4      ┆ ┆  5      ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1

### 2 {.col-span-2}

### 3

### 4

### 5
```

#### 第四个卡片跨越两列

```text
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆  1      ┆ ┆  2      ┆ ┆  3      ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆  4                  ┆ ┆  5      ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1

### 2

### 3

### 4 {.col-span-2}

### 5
```

### .row-span-2 {.row-span-2}

#### 第一个卡片跨越两行

```text
╭┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆ 1      ┆ ┆ 2       ┆ ┆ 3       ┆
┆        ┆ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
┆        ┆ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆        ┆ ┆ 4       ┆ ┆ 5       ┆
╰┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1 {.row-span-2}

### 2

### 3

### 4

### 5
```

#### 第二个卡片跨越两行

```text
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆ 1       ┆ ┆ 2      ┆ ┆ 3       ┆
╰┈┈┈┈┈┈┈┈┈╯ ┆        ┆ ╰┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈╮ ┆        ┆ ╭┈┈┈┈┈┈┈┈┈╮
┆ 4       ┆ ┆        ┆ ┆ 5       ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1

### 2 {.row-span-2}

### 3

### 4

### 5
```

#### 第三个卡片跨越两行

```text
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈╮
┆ 1       ┆ ┆ 2       ┆ ┆ 3      ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ┆        ┆
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ┆        ┆
┆ 4       ┆ ┆ 5       ┆ ┆        ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈╯
```

---

```markdown
### 1

### 2

### 3 {.row-span-2}

### 4

### 5
```

### .col-span-2 .row-span-2

```text
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆ 1                   ┆ ┆ 2       ┆
┆                     ┆ ╰┈┈┈┈┈┈┈┈┈╯
┆                     ┆ ╭┈┈┈┈┈┈┈┈┈╮
┆                     ┆ ┆ 3       ┆
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮ ╭┈┈┈┈┈┈┈┈┈╮
┆ 4       ┆ ┆ 5       ┆ ┆ 6       ┆
╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯ ╰┈┈┈┈┈┈┈┈┈╯
```

#### ↓ 源代码

```markdown
### 1 {.col-span-2 .row-span-2}

### 2

### 3

### 4

### 5
```

同时跨越行和列

## 表格变体

### 表格概览 {.secondary}

| -                | -                            |
| ---------------- | ---------------------------- |
| `{.show-header}` | 显示表格的表头 |
| `{.shortcuts}`   | 渲染快捷键样式    |
| `{.bold-first}`  | 加粗第一列            |
| `{.plus-first}`  | 第一列加号            |
| `{.show-header}` | 显示表头                 |
| `{.left-text}`   | 最后一列左对齐   |
| `{.no-wrap}`     | 不换行              |

### 基本表格

| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

#### ↓ 源代码

```markdown
| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |
```

### .shortcuts

| -          | -        |
| ---------- | -------- |
| `Ctrl` `N` | 新建文件 |
| `Ctrl` `S` | 保存     |

{.shortcuts}

#### ↓ 源代码

```markdown
| -          | -        |
| ---------- | -------- |
| `Ctrl` `N` | 新建文件 |
| `Ctrl` `S` | 保存     |

{.shortcuts}
```

### .show-header

| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.show-header}

#### ↓ 源代码

```markdown
| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.show-header}
```

### .left-text

| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.left-text}

#### ↓ 源代码

```markdown
| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.left-text}
```

### .bold-first

| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.bold-first}

#### ↓ 源代码

```markdown
| 模式  | 描述            |
| -------- | ---------------------- |
| `[abc]`  | 匹配 a, b 或 c        |
| `[^abc]` | 匹配除 a, b 或 c 之外的字符 |
| `[a-z]`  | 匹配 a 到 z           |

{.bold-first}
```

## 列表变体

### 列表概览 {.secondary}

列表列

| -           | -                      |
| ----------- | ---------------------- |
| `{.cols-1}` | 单列 _(默认)_ |
| `{.cols-2}` | 双列            |
| ...         |                        |
| `{.cols-6}` |                        |

列表标记

| -                    | -                          |
| -------------------- | -------------------------- |
| `{.marker-none}`     | 未设置标记          |
| `{.marker-timeline}` | 时间轴样式的标记 |
| `{.marker-round}`    | 圆形标记               |

### 单列 (默认)

- 分享快速参考。
- 开发人员速查表。
- 由开源天使贡献。
- 管理您的代码片段。

#### ↓ 源代码

```markdown
- 分享快速参考。
- 开发人员速查表。
- 由开源天使贡献。
- 管理您的代码片段。
```

### .cols-3

- 分享
- 快速
- 参考
- 和
- 速查表
- 为了
- 开发人员

{.cols-3}

#### ↓ 源代码

```markdown
- 分享
- 快速
- 参考
- 和
- 速查表
- 为了
- 开发人员

{.cols-3}
```

### .marker-timeline {.row-span-2}

- **重命名** 为 `new_name`
  ```shell script
  $ git branch -m <new_name>
  ```
- **推送** 并重置
  ```shell script
  $ git push origin -u <new_name>
  ```
- **删除** 远程分支 `shell script     $ git push origin --delete <old>     `

{.marker-timeline}

#### ↓ 源代码

````markdown
- **重命名** 为 `new_name`
  ```shell script
  $ git branch -m <new_name>
  ```
- **推送** 并重置
  ```shell script
  $ git push origin -u <new_name>
  ```
- **删除** 远程分支 `shell script     $ git push origin --delete <old>     `

{.marker-timeline}
````

### .marker-none

- 分享
- 快速
- 参考
- 和
- 速查表

{.cols-2 .marker-none}

#### ↓ 源代码

```markdown
- 分享
- 快速
- 参考
- 和
- 速查表

{.cols-2 .marker-none}
```

### .marker-round

- 分享
- 快速
- 参考

{.marker-round}

#### ↓ 源代码

```markdown
- 分享
- 快速
- 参考

{.marker-round}
```

## 代码变体

### 基本代码

```js
r3f.cn.is(() => {
  awesome.site();
});
```

```js
here.is.some.more();
```

#### ↓ 源代码

`````markdown
````js
r3f.cn.is(() => {
  awesome.site()
})
\```

```js
here.is.some.more()
\```
````
`````

代码块可以一个接一个地放置。

### 带标题的代码

#### index.js

```js
r3f.cn.is(() => {
  awesome.site();
});
```

#### other.js

```js
here.is.some.more();
```

#### ↓ 源代码

````markdown
#### index.js

```js
r3f.cn.is(() => {
  awesome.site();
});
```

#### other.js

```js
here.is.some.more();
```
````

代码块可以有标题。

### 换行

```js {.wrap}
<script>(function(d,s){if(window.Promise&&[].includes&&Object.assign&&window.Map)return;var js,sc=d.getElementsByTagName(s)[0];js=d.createElement(s);js.src='https://cdn.polyfill.io/v2/polyfill.min.js';sc.parentNode.insertBefore(js, sc);}(document,'script'))</script>
```

#### ↓ 源代码

````markdown {.wrap}
```js {.wrap}
<script>(function(d,s){if(window.Promise&&[].includes&&Object.assign&&window.Map)return;var js,sc=d.getElementsByTagName(s)[0];js=d.createElement(s);js.src='https://cdn.polyfill.io/v2/polyfill.min.js';sc.parentNode.insertBefore(js, sc);}(document,'script'))</script>
```
````

添加 `{.wrap}` 以换行长行。

### 长行 (默认)

```js
function createNode(nodeName: string, options: { key: string }) {
  return true
}
```

长行将有滚动条。

## 段落变体

### 头部段落

出现在头部的文本

#### ↓ 源代码

```markdown {.wrap}
### 基本段落

出现在头部的文本
```

### 中间段落 {.row-span-2}

- 这是一个列表

此段落将出现在中间

```js
cheatsheets.is(() => {
  awesome.site();
});
```

#### ↓ 源代码

````markdown
### 中间段落

- 这是一个列表

此段落将出现在中间

```js
cheatsheets.is(() => {
  awesome.site();
});
```
````

### 尾部段落 {.row-span-2}

```js
cheatsheets.is(() => {
  awesome.site();
});
```

#### ↓ 源代码

````markdown
```js
cheatsheets.is(() => {
  awesome.site();
});
```

此段落将出现在尾部
````

此段落将出现在尾部

### 交叉链接

添加 `{.link-arrow}` 以创建醒目的外部链接：

```js
[主页](/) {.link-arrow}
```

[主页](/) {.link-arrow}

## 卡片示例

### row-span-2 {.row-span-2}

```
1
```

### col-span-2 {.col-span-2}

```
2
```

### 主卡片 {.primary}

```
3
```

添加 `{.primary}` 使标题变为红色。

### 次要卡片 {.secondary}

```
4
```

添加 `{.secondary}` 使标题变为黄色。

### col-span-3 {.col-span-3}

```
5
```

