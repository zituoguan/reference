---
title: Express
date: 2023-02-26 15:23:31
background: bg-[#edc545]
tags:
  - config
  - format
categories:
  - 编程
intro: |
  Express 快速参考备忘单，一个灵活且简化的 Node.js Web 框架。
plugins:
  - copyCode
---

## 快速入门

### Hello World {.row-span-2}

- "创建项目，添加 `package.json` 配置

  ```bash
  $ mkdir myapp # 创建目录
  $ cd myapp    # 进入目录
  $ npm init -y # 初始化配置
  ```

- 安装依赖

  ```bash
  $ npm install express
  ```

- 入口文件 `index.js` 添加代码：

  ```js
  const express = require("express");
  const app = express();
  const port = 3000;
  app.get("/", (req, res) => {
    res.send("Hello World!");
  });
  app.listen(port, () => {
    console.log(`监听端口 ${port}`);
  });
  ```

- 使用以下命令运行应用程序
  ```bash
  $ node index.js
  ```
  {.marker-timeline}

### express -h {.row-span-2}

```bash
用法: express [选项] [目录]
选项:
  -h, --help 输出用法信息
      --version 输出版本号
  -e, --ejs 添加 ejs 引擎支持
      --hbs 添加 hbs 引擎支持
      --pug 添加 pug 引擎支持
  -H, --hogan 添加 hogan.js 引擎支持
      --no-view 不生成视图引擎
  -v, --view <引擎> 添加视图 <引擎> 支持 (ejs|hbs|hjs|jade|pug|twig|vash) (默认为 jade)
  -c, --css <引擎> 添加样式表 <引擎> 支持 (less|stylus|compass|sass) (默认为 css)
      --git 添加 .gitignore
  -f, --force 强制操作非空目录
```

{.wrap-text}

创建一个 `myapp` 项目

```bash
$ express --view=pug myapp
# 运行应用程序
$ DEBUG=myapp:*npm start
```

### express()

| :-                     | :-                                                          |
| :--------------------- | :---------------------------------------------------------- |
| `express.json()`       | [#](http://expressjs.com/en/4x/api.html#express.json)       |
| `express.raw()`        | [#](http://expressjs.com/en/4x/api.html#express.raw)        |
| `express.Router()`     | [#](http://expressjs.com/en/4x/api.html#express.router)     |
| `express.static()`     | [#](http://expressjs.com/en/4x/api.html#express.static)     |
| `express.text()`       | [#](http://expressjs.com/en/4x/api.html#express.text)       |
| `express.urlencoded()` | [#](http://expressjs.com/en/4x/api.html#express.urlencoded) |

### 路由 (Router)

| :-                | :-                                                     |
| :---------------- | :----------------------------------------------------- |
| `router.all()`    | [#](http://expressjs.com/en/4x/api.html#router.all)    |
| `router.METHOD()` | [#](http://expressjs.com/en/4x/api.html#router.METHOD) |
| `router.param()`  | [#](http://expressjs.com/en/4x/api.html#router.param)  |
| `router.route()`  | [#](http://expressjs.com/en/4x/api.html#router.route)  |
| `router.use()`    | [#](http://expressjs.com/en/4x/api.html#router.use)    |

### 应用程序 (Application)

```js
var express = require("express");
var app = express();

console.dir(app.locals.title);
//=> 'My App'
console.dir(app.locals.email);
//=> 'me@myapp.com'
```

#### 属性 (Attribute)

| :-              | :-                                                                                        |
| :-------------- | :---------------------------------------------------------------------------------------- |
| `app.locals`    | 应用程序中的局部变量 [#](http://expressjs.com/en/4x/api.html#app.locals)    |
| `app.mountpath` | 用于挂载子应用程序的路径模式 [#](http://expressjs.com/en/4x/api.html#app.mountpath) |

#### 事件 (Events)

| :-      | :-                                                                                                                                                                   |
| :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `mount` | 子应用程序挂载到父应用程序时，在子应用程序上触发该事件 [#](http://expressjs.com/en/4x/api.html#app.onmount) |

#### 方法 (Method)

| :-                        | :-                                                         |
| :------------------------ | :--------------------------------------------------------- |
| `app.all()`               | [#](http://expressjs.com/en/4x/api.html#app.all)           |
| `app.delete()`            | [#](http://expressjs.com/en/4x/api.html#app.delete.method) |
| `app.disable()`           | [#](http://expressjs.com/en/4x/api.html#app.disable)       |
| `app.disabled()`          | [#](http://expressjs.com/en/4x/api.html#app.disabled)      |
| `app.enable()`            | [#](http://expressjs.com/en/4x/api.html#app.enable)        |
| `app.enabled()`           | [#](http://expressjs.com/en/4x/api.html#app.enabled)       |
| `app.engine()`            | [#](http://expressjs.com/en/4x/api.html#app.engine)        |
| `app.get(name)`           | [#](http://expressjs.com/en/4x/api.html#app.get)           |
| `app.get(path, callback)` | [#](http://expressjs.com/en/4x/api.html#app.get.method)    |
| `app.listen()`            | [#](http://expressjs.com/en/4x/api.html#app.listen)        |
| `app.METHOD()`            | [#](http://expressjs.com/en/4x/api.html#app.METHOD)        |
| `app.param()`             | [#](http://expressjs.com/en/4x/api.html#app.param)         |
| `app.path()`              | [#](http://expressjs.com/en/4x/api.html#app.path)          |
| `app.post()`              | [#](http://expressjs.com/en/4x/api.html#app.post.method)   |
| `app.put()`               | [#](http://expressjs.com/en/4x/api.html#app.put.method)    |
| `app.render()`            | [#](http://expressjs.com/en/4x/api.html#app.render)        |
| `app.route()`             | [#](http://expressjs.com/en/4x/api.html#app.route)         |
| `app.set()`               | [#](http://expressjs.com/en/4x/api.html#app.set)           |
| `app.use()`               | [#](http://expressjs.com/en/4x/api.html#app.use)           |

### 请求 (Request)

#### 属性 (Attribute)

| :-                  | :-                                                         |
| :------------------ | :--------------------------------------------------------- |
| `req.app`           | [#](http://expressjs.com/en/4x/api.html#req.app)           |
| `req.baseUrl`       | [#](http://expressjs.com/en/4x/api.html#req.baseUrl)       |
| `req.body`          | [#](http://expressjs.com/en/4x/api.html#req.body)          |
| `req.cookies`       | [#](http://expressjs.com/en/4x/api.html#req.cookies)       |
| `req.fresh`         | [#](http://expressjs.com/en/4x/api.html#req.fresh)         |
| `req.hostname`      | [#](http://expressjs.com/en/4x/api.html#req.hostname)      |
| `req.ip`            | [#](http://expressjs.com/en/4x/api.html#req.ip)            |
| `req.ips`           | [#](http://expressjs.com/en/4x/api.html#req.ips)           |
| `req.method`        | [#](http://expressjs.com/en/4x/api.html#req.method)        |
| `req.originalUrl`   | [#](http://expressjs.com/en/4x/api.html#req.originalUrl)   |
| `req.params`        | [#](http://expressjs.com/en/4x/api.html#req.params)        |
| `req.path`          | [#](http://expressjs.com/en/4x/api.html#req.path)          |
| `req.protocol`      | [#](http://expressjs.com/en/4x/api.html#req.protocol)      |
| `req.query`         | [#](http://expressjs.com/en/4x/api.html#req.query)         |
| `req.route`         | [#](http://expressjs.com/en/4x/api.html#req.route)         |
| `req.secure`        | [#](http://expressjs.com/en/4x/api.html#req.secure)        |
| `req.signedCookies` | [#](http://expressjs.com/en/4x/api.html#req.signedCookies) |
| `req.stale`         | [#](http://expressjs.com/en/4x/api.html#req.stale)         |
| `req.subdomains`    | [#](http://expressjs.com/en/4x/api.html#req.subdomains)    |
| `req.xhr`           | [#](http://expressjs.com/en/4x/api.html#req.xhr)           |

#### 方法 (Method)

| :-                       | :-                                                                              |
| :----------------------- | :------------------------------------------------------------------------------ |
| `req.accepts()`          | [#](http://expressjs.com/en/4x/api.html#req.accepts)                            |
| `req.acceptsCharsets()`  | [#](http://expressjs.com/en/4x/api.html#req.acceptsCharsets)                    |
| `req.acceptsEncodings()` | [#](http://expressjs.com/en/4x/api.html#req.acceptsEncodings)                   |
| `req.acceptsLanguages()` | [#](http://expressjs.com/en/4x/api.html#req.acceptsLanguages)                   |
| `req.get()`              | 获取 HTTP 请求头字段 [#](http://expressjs.com/en/4x/api.html#req.get) |
| `req.is()`               | [#](http://expressjs.com/en/4x/api.html#req.is)                                 |
| `req.param()`            | [#](http://expressjs.com/en/4x/api.html#req.param)                              |
| `req.range()`            | [#](http://expressjs.com/en/4x/api.html#req.range)                              |

### 响应 (Response)

```js
app.get("/", function (req, res) {
  console.dir(res.headersSent); //false
  res.send("OK");
  console.dir(res.headersSent); //true
});
```

#### 属性 (Attribute)

| :-                | :-                                                       |
| :---------------- | :------------------------------------------------------- |
| `res.app`         | [#](http://expressjs.com/en/4x/api.html#res.app)         |
| `res.headersSent` | [#](http://expressjs.com/en/4x/api.html#res.headersSent) |
| `res.locals`      | [#](http://expressjs.com/en/4x/api.html#res.locals)      |

#### 方法 (Method)

| :-                  | :-                                                                                    |
| :------------------ | :------------------------------------------------------------------------------------ |
| `res.append()`      | [#](http://expressjs.com/en/4x/api.html#res.append)                                   |
| `res.attachment()`  | [#](http://expressjs.com/en/4x/api.html#res.attachment)                               |
| `res.cookie()`      | [#](http://expressjs.com/en/4x/api.html#res.cookie)                                   |
| `res.clearCookie()` | [#](http://expressjs.com/en/4x/api.html#res.clearCookie)                              |
| `res.download()`    | 提示文件下载 [#](http://expressjs.com/en/4x/api.html#res.download)    |
| `res.end()`         | 结束响应过程 [#](http://expressjs.com/en/4x/api.html#res.end)             |
| `res.format()`      | [#](http://expressjs.com/en/4x/api.html#res.format)                                   |
| `res.get()`         | [#](http://expressjs.com/en/4x/api.html#res.get)                                      |
| `res.json()`        | 发送 JSON 响应 [#](http://expressjs.com/en/4x/api.html#res.json)                  |
| `res.jsonp()`       | 发送支持 JSONP 的响应 [#](http://expressjs.com/en/4x/api.html#res.jsonp) |
| `res.links()`       | [#](http://expressjs.com/en/4x/api.html#res.links)                                    |
| `res.location()`    | [#](http://expressjs.com/en/4x/api.html#res.location)                                 |
| `res.redirect()`    | 重定向请求 [#](http://expressjs.com/en/4x/api.html#res.redirect)                |
| `res.render()`      | 渲染视图模板 [#](http://expressjs.com/en/4x/api.html#res.render)              |
| `res.send()`        | 发送各种类型的响应 [#](http://expressjs.com/en/4x/api.html#res.send)     |
| `res.sendFile()`    | 以八位字节流形式发送文件 [#](http://expressjs.com/en/4x/api.html#res.sendFile)  |
| `res.sendStatus()`  | [#](http://expressjs.com/en/4x/api.html#res.sendStatus)                               |
| `res.set()`         | [#](http://expressjs.com/en/4x/api.html#res.set)                                      |
| `res.status()`      | [#](http://expressjs.com/en/4x/api.html#res.status)                                   |
| `res.type()`        | [#](http://expressjs.com/en/4x/api.html#res.type)                                     |
| `res.vary()`        | [#](http://expressjs.com/en/4x/api.html#res.vary)                                     |

## 示例 (Example)

### 路由 (Router) {. row-span-2}

对传递给此路由器的任何请求调用

```js
router.use(function (req, res, next) {
  //.. 一些逻辑在这里 .. 像任何其他中间件一样
  next();
});
```

将处理任何以 `/events` 结尾的请求

```js
//取决于路由器 "use()" 的位置
router.get("/events", (req, res, next) => {
  //..
});
```

### 响应 (Response)

`res` 对象表示 `Express` 应用程序在收到 HTTP 请求时发送的 HTTP 响应

```js
app.get("/user/:id", (req, res) => {
  res.send("user" + req.params.id);
});
```

### 请求 (Request)

`req` 对象表示一个 `HTTP` 请求，并具有请求查询字符串、参数、正文、HTTP
头等属性。

```js
app.get("/user/:id", (req, res) => {
  res.send("user" + req.params.id);
});
```

### res.end()

```js
res.end();
res.status(404).end();
```

结束响应过程。此方法实际上来自 Node 核心，特别是
`http.ServerResponse` 的 `response.end()` 方法。

### res.json([body])

```js
res.json(null);
res.json({ user: "tobi" });
res.status(500).json({ error: "message" });
```

### app.all

```js
app.all("/secret", function (req, res, next) {
  console.log("访问秘密区域...");
  next(); // 将控制权传递给下一个处理程序
});
```

### app.delete

```js
app.delete("/", function (req, res) {
  res.send("向主页发出 DELETE 请求");
});
```

### app.disable(name)

```js
app.disable("trust proxy");
app.get("trust proxy");
// => false
```

### app.disabled(name)

```js
app.disabled("trust proxy");
// => true

app.enable("trust proxy");
app.disabled("trust proxy");
// => false
```

### app.engine(ext, callback)

```js
var engines = require("consolidate");

app.engine("haml", engines.haml);
app.engine("html", engines.hogan);
```

### app.listen([port[, host[, backlog]]][, callback])

```js
var express = require("express");

var app = express();
app.listen(3000);
```

### 路由 (Routing)

```js
const express = require("express");
const app = express();

//向主页发出 GET 请求时响应 "hello world"
app.get("/", (req, res) => {
  res.send("hello world");
});
```

```js
// GET 方法路由
app.get("/", (req, res) => {
  res.send("向主页发出 GET 请求");
});

// POST 方法路由
app.post("/", (req, res) => {
  res.send("向主页发出 POST 请求");
});
```

### 中间件 (Middleware)

```js
function logOriginalUrl(req, res, next) {
  console.log("请求URL:", req.originalUrl);
  next();
}

function logMethod(req, res, next) {
  console.log("请求类型:", req.method);
  next();
}

const log = [logOriginalUrl, logMethod];

app.get("/user/:id", log, (req, res, next) => {
  res.send("用户信息");
});
```

### 使用模板 (Using templates)

```js
app.set("view engine", "pug");
```

在 `views` 目录中创建一个名为 `index.pug` 的 `Pug` 模板文件，内容如下：

```pug
html
  head
    title= title
  body
    h1=message
```

创建一个路由来渲染 `index.pug` 文件。如果未设置视图引擎属性，则必须指定视图文件的扩展名。

```js
app.get("/", (req, res) => {
  res.render("index", {
    title: "嘿",
    message: "你好！",
  });
});
```
