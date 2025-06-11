---
title: HTMX
date: 2025-06-07 19:30:00
background: bg-[#ff5f4d]
tags:
  - 前端
  - javascript
  - htmx
categories:
  - 编程
intro: |
  一个现代、简约的 JavaScript 库，它允许您使用 HTML 属性来创建动态的 Web 界面。
plugins:
  - copyCode
---

## 开始使用 {.cols-3}

### CDN 导入

```html
<script src="https://unpkg.com/htmx.org@1.9.2"></script>
```

### 基本用法

```html
<button
  hx-get="/hello"
  hx-target="#result">
  打个招呼
</button>
<div id="result"></div>
```

### 服务器响应

```html
<!-- /hello 响应 -->
<p>来自服务器的问候</p>
```

## 核心属性 {.cols-3}

### `hx-get`, `hx-post` 等

```html
<a hx-get="/page">加载页面</a>
<form hx-post="/submit"></form>
```

### `hx-target`

```html
<button hx-get="/data" hx-target="#box"></button>
<div id="box"></div>
```

### `hx-trigger`

```html
<input
  hx-get="/search"
  hx-trigger="keyup changed delay:300ms"
  hx-target="#results" />
```

## Swap（交换）与 Out of Band（带外） {.cols-3}

### `hx-swap`

```html
<div
  hx-get="/frag"
  hx-swap="innerHTML">
</div>
```

* `outerHTML`
* `innerHTML`
* `beforebegin`, `afterbegin` 等

### `hx-swap-oob`

```html
<div hx-swap-oob="true" id="msg"></div>
```

*适用于通过局部视图进行全局更新。*

### Swap 修饰符

```html
hx-swap="outerHTML transition:true swap:1s"
```

## 表单与事件 {.cols-3}

### 提交时自动 POST

```html
<form hx-post="/submit" hx-target="#status">
  <input name="name" />
  <button type="submit">发送</button>
</form>
<div id="status"></div>
```

### `hx-include`

```html
<input id="user-id" name="id" />
<button
  hx-post="/update"
  hx-include="#user-id">
  更新
</button>
```

### `hx-vals`

```html
<button
  hx-post="/save"
  hx-vals='{"id": 42, "active": true}'>
  保存
</button>
```

## 高级功能 {.cols-3}

### 加载指示器

```html
<button
  hx-get="/load"
  hx-indicator="#spinner">
  加载
</button>
<div id="spinner" class="htmx-indicator">加载中...</div>
```

### `hx-push-url`

```html
<a hx-get="/page" hx-push-url="true">前往</a>
```

### 轮询

```html
<div hx-get="/time" hx-trigger="every 5s"></div>
```

## 事件与扩展 {.cols-3}

### 监听事件

```js
document.body.addEventListener('htmx:afterSwap', e => {
  console.log("交换完成");
});
```

### 事件钩子

* `htmx:beforeRequest`
* `htmx:afterSwap`
* `htmx:responseError`

### 扩展

```html
<script src="https://unpkg.com/htmx.org/dist/ext/json-enc.js"></script>
<form hx-post="/api" hx-ext="json-enc"></form>
```

## 示例用例 {.cols-2}

### Python 后端 (Flask)

```python
@app.route("/hello")
def hello():
    return "<p>你好，HTMX！</p>"
```

### HTML 客户端

```html
<button
  hx-get="/hello"
  hx-target="#msg">
  点击
</button>
<div id="msg"></div>
```
