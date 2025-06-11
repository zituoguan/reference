---
title: EJS
date: 2023-04-07
background: bg-[#b4ca65]
tags:
  - EJS
  - 前端
  - 框架
categories:
  - 编程
intro:
  EJS (嵌入式 JavaScript) 是一种简单的模板语言，它允许您使用纯 JavaScript 生成 HTML 标记。
plugins:
  - copyCode
  - runCode
---

<!-- 注意：EJS 不支持 Prettier，因此请手动格式化并在损坏的代码块上方添加 prettier-ignore -->

## 开始使用 { .cols-3 }

### Hello world

#### 安装

```shell
$ npm install ejs
```

#### hello.ejs

<!-- prettier-ignore -->
```html
<% if (user.email) { %>
  <h1><%= user.email %></h1>
<% } %>
```

#### CLI

```shell
$ ejs hello.ejs -o hello.html
```

### 使用数据渲染

```js
let ejs = require("ejs");

let people = ["geddy", "neil", "alex"];
let tpl = '<%= people.join(", "); %>';

let html = ejs.render(tpl, { people: people });
console.log(html);
```

向 EJS 传递模板字符串和一些数据。

### 浏览器支持

```html
<script src="https://unpkg.com/ejs"></script>
<script>
  let people = ["geddy", "neil", "alex"];
  let html = ejs.render('<%= people.join(", "); %>', { people: people });
  console.log(html);
</script>
```

在 script 标签中使用 ejs。

### 变量

|              |                                  |
| ------------ | -------------------------------- |
| `<%= var %>` | 打印变量的值                     |
| `<%- var %>` | 打印值（不进行 HTML 转义）       |

### CLI

渲染并指定输出文件。

```shell
$ ejs hello.ejs -o hello.html
```

为其提供模板文件和数据文件

```shell
$ ejs hello.ejs -f data.json -o hello.html
```

### 注释

```html
<%# 这行将表示一个注释 %>
```

---

<!-- prettier-ignore -->
```html
<%# 这是一个多行 EJS 注释。
    它可以跨越多行，
    但不会在最终的 HTML 输出中显示。
%>
```

### 方法 {.col-span-2}

```js
let ejs = require("ejs");
let template = ejs.compile(str, options);

template(data);
// => 渲染后的 HTML 字符串

ejs.render(str, data, options);
// => 渲染后的 HTML 字符串

ejs.renderFile(filename, data, options, function (err, str) {
  // str => 渲染后的 HTML 字符串
});
```

### 包含文件

```html
<%- include('partials/navbar.ejs') %>
```

包含带数据的模板：

```html
<% include('header', { title: 'My Page' }) %>
```

---

<!-- prettier-ignore -->
```html
<ul>
  <% users.forEach(function(user){ %>
    <%- include('item', {user: user}); %>
  <% }); %>
</ul>
```

要包含模板，需要文件名选项，路径是相对的。

## 文档 {.cols-3}

### 条件语句

<!-- prettier-ignore -->
```html
<% if (userLoggedIn) { %>
  <p>欢迎, <%= username %>!</p>
<% } else { %>
  <p>请登录。</p>
<% } %>
```

### 使用循环

<!-- prettier-ignore -->
```html
<ul>
  <% for(i=0; i < users.length; i++) { %>
    <li><%= users[i].username %></li>
  <% } %>
</ul>
```

### 自定义分隔符

```js
let ejs = require("ejs"),
  users = ["geddy", "neil", "alex"];

// 仅单个模板
ejs.render('<?= users.join(" | "); ?>', { users: users }, { delimiter: "?" });
// => 'geddy | neil | alex'

// 或全局设置
ejs.delimiter = "$";
ejs.render('<$= users.join(" | "); $>', { users: users });
// => 'geddy | neil | alex'
```

### 缓存

```js
let ejs = require("ejs"),
  LRU = require("lru-cache");

// LRU 缓存，限制 100 项
ejs.cache = LRU(100);
```

### 自定义文件加载器

```js
let ejs = require("ejs");
let myFileLoader = function (filePath) {
  return "myFileLoader: " + fs.readFileSync(filePath);
};

ejs.fileLoader = myFileLoader;
```

### 布局

<!-- prettier-ignore -->
```html
<%- include('header'); -%>
<h1>
  标题
</h1>
<p>
  我的页面
</p>
<%- include('footer'); -%>
```

## 客户端支持 {.cols-2}

### 示例

```html
<div id="output"></div>
<script src="ejs.min.js"></script>
<script>
  let people = ["geddy", "neil", "alex"],
    html = ejs.render('<%= people.join(", "); %>', { people: people });
  // 使用 jQuery:
  $("#output").html(html);
  // 原生 JS:
  document.getElementById("output").innerHTML = html;
</script>
```

### 注意事项

```js
let str = "Hello <%= include('file', {person: 'John'}); %>",
  fn = ejs.compile(str, { client: true });

// include 回调
fn(data, null, function (path, d) {
  // path -> 'file'
  // d -> {person: 'John'}
  // 在此处放置您的代码
  // 以字符串形式返回文件内容
}); // 返回渲染后的字符串
```

## 选项 {.cols-1}

### 选项列表

| 选项               | 描述                                                                                                                                                                                                                          |
| ------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cache              | 编译后的函数会被缓存，需要文件名                                                                                                                                                                                                  |
| filename           | 缓存用于键控缓存以及包含文件时使用                                                                                                                                                                                                |
| root               | 为包含文件设置项目根目录的绝对路径（例如 `/file.ejs`）。可以是一个数组，尝试从多个目录解析包含文件。                                                                                                                                      |
| views              | 解析相对路径的包含文件时使用的路径数组。                                                                                                                                                                                            |
| context            | 函数执行上下文                                                                                                                                                                                                                  |
| compileDebug       | 当为 false 时，不编译调试工具                                                                                                                                                                                                     |
| client             | 返回独立的编译函数                                                                                                                                                                                                                |
| delimiter          | 用于内部界定符的字符，默认为 `%`                                                                                                                                                                                                    |
| openDelimiter      | 用于开始界定符的字符，默认为 `<`                                                                                                                                                                                                    |
| closeDelimiter     | 用于结束界定符的字符，默认为 `>`                                                                                                                                                                                                    |
| debug              | 输出生成的函数体                                                                                                                                                                                                                  |
| strict             | 当设置为 `true` 时，生成的函数处于严格模式                                                                                                                                                                                              |
| \_with             | 是否使用 `with() {}` 结构。如果为 `false`，则局部变量将存储在 `locals` 对象中。（意味着 `--strict`）                                                                                                                                    |
| localsName         | 不使用 `with` 时，用于存储局部变量的对象的名称，默认为 `locals`                                                                                                                                                                           |
| rmWhitespace       | 移除所有可安全移除的空白字符，包括前导和尾随空白。它还为所有 scriptlet 标签启用更安全的 `-%>` 行吞噬版本（它不会剥离行中间标签的换行符）。                                                                                             |
| escape             | 与 `<%=` 结构一起使用的转义函数。它用于渲染，并在生成客户端函数时会对其调用 `.toString()`。（默认转义 XML）。                                                                                                                            |
| outputFunctionName | 设置为一个字符串（例如，'echo' 或 'print'），用于在 scriptlet 标签内打印输出的函数。                                                                                                                                               |
| async              | 当为 true 时，EJS 将使用异步函数进行渲染。（取决于 JS 运行时中对 async/await 的支持。）                                                                                                                                             |

## 标签 {.cols-1}

### 标签列表

| 标签              | 描述                                                                 |
| ----------------- | :------------------------------------------------------------------- |
| `<%`              | 'Scriptlet' 标签，用于控制流，无输出                                 |
| <code><%\_</code> | '空白吞噬' Scriptlet 标签，去除其前的所有空白字符                       |
| `<%=`             | 将值输出到模板中（HTML 转义）                                        |
| `<%-`             | 将未转义的值输出到模板中                                             |
| `<%#`             | 注释标签，不执行，无输出                                             |
| `<%%`             | 输出字面量的 `<%`                                                    |
| `%>`              | 普通结束标签                                                         |
| `-%>`             | Trim-mode ('换行吞噬') 标签，去除其后的换行符                      |
| <code>\_%></code> | '空白吞噬' 结束标签，去除其后的所有空白字符                             |

## CLI {.cols-1}

### CLI 列表

| 选项                               | 描述                                                                                        |
| ------------------------------------ | :------------------------------------------------------------------------------------------ |
| `cache`                              | 编译后的函数会被缓存，需要文件名                                                              |
| `-o` / `--output-file FILE`          | 将渲染的输出写入 FILE 而不是标准输出。                                                        |
| `-f` / `--data-file FILE`            | 必须是 JSON 格式。使用来自 FILE 的解析输入作为渲染数据。                                      |
| `-i` / `--data-input STRING`         | 必须是 JSON 格式且经过 URI 编码。使用来自 STRING 的解析输入作为渲染数据。                       |
| `-m` / `--delimiter CHARACTER`       | 使用 CHARACTER 和尖括号作为开始/结束（默认为 %）。                                            |
| `-p` / `--open-delimiter CHARACTER`  | 使用 CHARACTER 代替左尖括号作为开始。                                                         |
| `-c` / `--close-delimiter CHARACTER` | 使用 CHARACTER 代替右尖括号作为结束。                                                         |
| `-s` / `--strict`                    | 当设置为 `true` 时，生成的函数处于严格模式                                                      |
| `-n` / `--no-with`                   | 使用 `locals` 对象存储变量，而不是使用 `with`（意味着 --strict）。                                |
| `-l` / `--locals-name`               | 不使用 `with` 时，用于存储局部变量的对象的名称。                                                |
| `-w` / `--rm-whitespace`             | 移除所有可安全移除的空白字符，包括前导和尾随空白。                                            |
| `-d` / `--debug`                     | 输出生成的函数体                                                                              |
| `-h` / `--help`                      | 显示此帮助信息。                                                                              |
| `-V` / `-v` / `--version`            | 显示 EJS 版本。                                                                             |

使用示例：

```shell
$ ejs -p [ -c ] ./template_file.ejs -o ./output.html
$ ejs ./test/fixtures/user.ejs name=Lerxst
$ ejs -n -l _ ./some_template.ejs -f ./data_file.json
```
