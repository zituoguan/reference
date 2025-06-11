---
title: Mitmproxy
date: 2020-12-22 20:10:08
background: bg-[#d86138]
tags:
  - capture
  - traffic
  - network
  - utility
categories:
  - 工具箱
intro: |
  [mitmproxy](https://mitmproxy.org/) 是一款免费且开源的交互式 HTTPS 代理工具。这是一份 mitmproxy 的快速参考备忘单。
plugins:
  - copyCode
---

## 入门指南

### 用法 {.col-span-2}

| 选项 | 示例                                               | 描述                                      |
| ---- | -------------------------------------------------- | ----------------------------------------- |
| `-p` | mitmproxy -p 8001                                  | 在端口 8001 上启动代理                    |
| `-m` | mitmproxy -p 8001 -m reverse:http://127.0.0.1:4000 | 在端口 8001 上反向代理到端口 4000         |
| `-w` | mitmproxy -p 8001 -w traffic.mitm                  | 数据流到达时将其流式传输到文件              |
| `-r` | mitmproxy -r traffic.mitm                          | 从文件读取数据流                          |
| `-C` | mitmproxy -C traffic.mitm                          | 从保存的文件中重放客户端请求              |
| `-S` | mitmproxy -S traffic.mitm                          | 从保存的文件中重放服务器响应              |
| `-s` | mitmproxy -s myScript.py                           | 执行脚本                                  |
| `-h` | mitmproxy -h                                       | mitmproxy 快速帮助                        |

### 移动

```
        k                 Ctrl b
        ▲                   ▲▲
        │                   ││
h ◀ ─── + ─── ▶ l           ││ 页面
        │                   ││
        ▼                   ▼▼
        j             Ctrl f / 空格
```

---

| -                    | -                       |
| -------------------- | ----------------------- |
| `h`, `j`, `k` ,`l`   | 左, 下, 上, 右          |
| `Ctrl` `b`           | 上一页                  |
| `空格` / `Ctrl` `f`  | 下一页                  |
| `g` / `G`            | 跳转到开头 / 结尾       |
| `方向键`             | 上, 下, 左, 右          |

{.shortcuts}

### 复制到剪贴板

命令语法：

```
:export.clip format flow
```

---

示例：

| 描述                       | 命令示例                           |
| -------------------------- | ---------------------------------- |
| 1. 复制为 curl 命令        | `:export.clip curl @focus`         |
| 2. 复制为 httpie           | `:export.clip httpie @focus`       |
| 2. 复制为原始数据          | `:export.clip raw @focus`          |
| 2. 复制为原始 HTTP 请求    | `:export.clip raw_request @focus`  |
| 2. 复制为原始 HTTP 响应    | `:export.clip raw_response @focus` |

{.style-list}

将数据流导出到系统剪贴板。

### 保存到文件

命令语法：

```
:export.file format flow path
```

---

示例：

| 描述                         | 命令示例                                           |
| ---------------------------- | -------------------------------------------------- |
| 1. 导出到 /tmp/a.curl        | `:export.file curl @focus /tmp/a.curl`             |
| 2. 导出到 /tmp/a.httpie      | `:export.file httpie @focus /tmp/a.httpie`         |
| 2. 导出到 /tmp/a.raw         | `:export.file raw @focus  /tmp/a.raw`              |
| 2. 导出到 /tmp/a.request     | `:export.file raw_request @focus /tmp/a.request`   |
| 2. 导出到 /tmp/a.response    | `:export.file raw_response @focus /tmp/a.response` |

{.style-list}

将数据流导出到系统剪贴板。

### 常用快捷键

| -       | -                |
| ------- | ---------------- |
| `q`     | 返回 / 退出      |
| `z`     | 清空数据流列表   |
| `:`     | 命令提示符       |
| `E`     | 查看事件日志     |
| `O`     | 查看选项         |
| `r`     | 重放此数据流     |
| `Tab`   | 下一个           |
| `Enter` | 选择             |

{.shortcuts}

### 全局快捷键

| -              | -                         |
| -------------- | ------------------------- |
| `-`            | 切换到下一个布局          |
| `?`            | 查看帮助                  |
| `B`            | 启动附加浏览器            |
| `C`            | 查看命令                  |
| `I`            | 切换拦截状态              |
| `K`            | 查看快捷键绑定            |
| `P`            | 查看数据流详情            |
| `Q`            | 立即退出                  |
| `W`            | 流式传输到文件            |
| `i`            | 设置拦截                  |
| `Ctrl` `右`    | 聚焦下一个布局窗格        |
| `Shift` `tab`  | 聚焦下一个布局窗格        |

{.shortcuts}

### 数据流 (视图)

| -               | -                            |
| --------------- | ---------------------------- |
| `A`             | 恢复所有被拦截的数据流       |
| `D`             | 复制数据流                   |
| `F`             | 设置焦点跟随                 |
| `L`             | 从文件加载数据流             |
| `M`             | 切换查看已标记的数据流       |
| `S`             | 开始服务器重放               |
| `U`             | 取消所有标记                 |
| `V`             | 还原对此数据流的更改         |
| `X`             | 终止此数据流                 |
| `Z`             | 清除所有未显示的数据流       |
| `a`             | 恢复此被拦截的数据流         |
| `b`             | 将响应体保存到文件           |
| `d`             | 从视图中删除数据流           |
| `e`             | 将此数据流导出到文件         |
| `f`             | 设置视图过滤器               |
| `m`             | 切换此数据流的标记状态       |
| `n`             | 创建一个新的数据流           |
| `o`             | 设置数据流列表顺序           |
| `r`             | 重放此数据流                 |
| `v`             | 反转数据流列表顺序           |
| `w`             | 将列出的数据流保存到文件     |
| <code>\|</code> | 在此数据流上运行脚本         |
| `Ctrl` `l`      | 将剪切内容发送到剪贴板       |

{.shortcuts}

## Mitmproxy 过滤器

### 过滤器

| -   | -                                     |
| --- | ------------------------------------- |
| `f` | 设置视图过滤器 _(在数据流视图页面)_   |

{.shortcuts}

---

- [正则表达式备忘单](/regex) _(r3f.cn)_

正则表达式是 Python 风格的，可以指定为带引号的字符串。

### 运算符

| -       | -         |
| ------- | --------- | --- |
| `!`     | 一元非    |
| `&`     | 与        |
| `       | `         | 或  |
| `(...)` | 分组      |

### 表达式 {.row-span-2}

| -              | -                                                          |
| -------------- | ---------------------------------------------------------- |
| `~a`           | 匹配响应中的资源：CSS、Javascript、Flash、图像。           |
| `~b` `regex`   | 主体                                                       |
| `~bq` `regex`  | 请求主体                                                   |
| `~bs` `regex`  | 响应主体                                                   |
| `~c` `int`     | HTTP 响应代码                                              |
| `~d` `regex`   | 域名                                                       |
| `~dst` `regex` | 匹配目标地址                                               |
| `~e`           | 匹配错误                                                   |
| `~h` `regex`   | 头部                                                       |
| `~hq` `regex`  | 请求头部                                                   |
| `~hs` `regex`  | 响应头部                                                   |
| `~http`        | 匹配 HTTP 数据流                                           |
| `~m` `regex`   | 方法                                                       |
| `~marked`      | 匹配已标记的数据流                                         |
| `~q`           | 匹配没有响应的请求                                         |
| `~s`           | 匹配响应                                                   |
| `~src` `regex` | 匹配源地址                                                 |
| `~t` `regex`   | Content-type 头部                                          |
| `~tcp`         | 匹配 TCP 数据流                                            |
| `~tq` `regex`  | 请求 Content-Type 头部                                     |
| `~ts` `regex`  | 响应 Content-Type 头部                                     |
| `~u` `regex`   | URL                                                        |
| `~websocket`   | 匹配 WebSocket 数据流 (以及 HTTP-WebSocket 握手数据流)     |

### 数据流选择器

表达式

| -           | -                          |
| ----------- | -------------------------- |
| `@all     ` | 所有数据流                 |
| `@focus   ` | 当前聚焦的数据流           |
| `@shown   ` | 当前显示的所有数据流       |
| `@hidden  ` | 当前隐藏的所有数据流       |
| `@marked  ` | 所有已标记的数据流         |
| `@unmarked` | 所有未标记的数据流         |

mitmproxy 有一组方便的数据流选择器，可对当前视图进行操作。

### 示例

URL 包含 "google.com"

```
google\.com
```

请求体包含字符串 "test" 的请求

```
~q ~b test
```

除了 content type 为 text/html 的请求之外的所有内容：

```
!(~q & ~t "text/html")
```

替换请求中的整个 GET 字符串 (需要引号才能使其工作)：

```
":~q ~m GET:.*:/replacement.html"
```

## Mitmproxy 脚本 {.cols-2}

### 自定义响应

```python
from mitmproxy import http


def request(flow: http.HTTPFlow) -> None:
    if flow.request.pretty_url == "http://example.com/path":
        flow.response = http.HTTPResponse.make(
            200,  # (可选) 状态码
            b"Hello World",  # (可选) 内容
            {"Content-Type": "text/html"}  # (可选) 头部
        )
```

从代理发送回复，而不向远程服务器发送任何数据。

### 添加头部

```python
class AddHeader:
    def __init__(self):
        self.num = 0

    def response(self, flow):
        self.num = self.num + 1
        flow.response.headers["count"] = str(self.num)


addons = [
    AddHeader()
]
```

向每个响应添加一个 HTTP 头部。

## 另请参阅

- [mitmproxy 插件](https://github.com/mitmproxy/mitmproxy/tree/master/examples/addons) _(github.com)_
- [mitmproxy 文档](https://docs.mitmproxy.org/) _(mitmproxy.org)_

