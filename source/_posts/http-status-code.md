---
title: HTTP 状态码
background: bg-[#3b7dc0]
date: 2020-12-26 16:09:09
tags:
  - 响应
  - 服务器
categories:
  - 其他
intro: |
  HTTP 状态码速查表。每个 HTTP 状态码的快速参考。
plugins:
  - tooltip
---

## HTTP 状态码

### 含义

<!-- prettier-ignore -->
- [1xx: 信息性状态码](#1xx-information){data-tooltip="表示请求已接收，继续处理。"}
- [2xx: 成功状态码](#2xx-successful){data-tooltip="表示操作已成功接收、理解并接受。"}
- [3xx: 重定向状态码](#3xx-redirection){data-tooltip="表示需要进一步操作以完成请求。"}
- [4xx: 客户端错误状态码](#4xx-client-error){data-tooltip="表示请求包含错误语法或无法完成。"}
- [5xx: 服务器错误状态码](#5xx-server-error){data-tooltip="表示服务器未能完成一个看似有效的请求。"}

### 2xx. 成功状态码 {.row-span-2}

<!-- prettier-ignore -->
- [200: OK](https://tools.ietf.org/html/rfc7231#section-6.3.1){data-tooltip="请求成功。"}
- [201: 已创建](https://tools.ietf.org/html/rfc7231#section-6.3.2){data-tooltip="请求完成，并创建了新资源。"}
- [202: 已接受](https://tools.ietf.org/html/rfc7231#section-6.3.3){data-tooltip="请求已接受处理，但处理尚未完成。"}
- [203: 非授权信息](https://tools.ietf.org/html/rfc7231#section-6.3.4){data-tooltip="实体头中的信息来自本地或第三方副本，而非原始服务器。"}
- [204: 无内容](https://tools.ietf.org/html/rfc7231#section-6.3.5){data-tooltip="响应中给出了状态码和头部，但回复中没有实体主体。"}
- [205: 重置内容](https://tools.ietf.org/html/rfc7231#section-6.3.6){data-tooltip="浏览器应清除用于此事务的表单以进行额外输入。"}
- [206: 部分内容](https://tools.ietf.org/html/rfc7233#section-4.1){data-tooltip="服务器正在返回所请求大小的部分数据。用于响应指定 Range 头的请求。服务器必须使用 Content-Range 头指定响应中包含的范围。"}
- [207: 多状态](https://tools.ietf.org/html/rfc4918#section-11.1){data-tooltip="为多个独立操作提供状态。"}
- [208: 已报告](https://tools.ietf.org/html/rfc5842#section-7.1){data-tooltip="在 DAV: propstat 响应元素内部使用，以避免重复枚举到同一集合的多个绑定的内部成员。"}
- [226: IM 已使用](https://tools.ietf.org/html/rfc3229#section-10.4.1){data-tooltip="服务器已完成对资源的请求，响应是应用于当前实例的一个或多个实例操作结果的表示。"}

### 4xx. 客户端错误状态码 {.row-span-3}

<!-- prettier-ignore -->
- [400: 错误请求](https://tools.ietf.org/html/rfc7231#section-6.5.1){data-tooltip="服务器无法理解该请求。"}
- [401: 未授权](https://tools.ietf.org/html/rfc7235#section-3.1){data-tooltip="请求的页面需要用户名和密码。"}
- [402: 需要付款](https://tools.ietf.org/html/rfc7231#section-6.5.2){data-tooltip="您尚不能使用此代码。"}
- [403: 禁止访问](https://tools.ietf.org/html/rfc7231#section-6.5.3){data-tooltip="禁止访问请求的页面。"}
- [404: 未找到](https://tools.ietf.org/html/rfc7231#section-6.5.4){data-tooltip="服务器找不到请求的页面。"}
- [405: 方法不允许](https://tools.ietf.org/html/rfc7231#section-6.5.5){data-tooltip="请求中指定的方法不被允许。"}
- [406: 不可接受](https://tools.ietf.org/html/rfc7231#section-6.5.6){data-tooltip="服务器只能生成客户端不接受的响应。"}
- [407: 需要代理身份验证](https://tools.ietf.org/html/rfc7235#section-3.2){data-tooltip="在处理此请求之前，您必须通过代理服务器进行身份验证。"}
- [408: 请求超时](https://tools.ietf.org/html/rfc7231#section-6.5.7){data-tooltip="请求花费的时间超过了服务器准备等待的时间。"}
- [409: 冲突](https://tools.ietf.org/html/rfc7231#section-6.5.8){data-tooltip="由于冲突，请求无法完成。"}
- [410: 已移除](https://tools.ietf.org/html/rfc7231#section-6.5.9){data-tooltip="请求的页面不再可用。"}
- [411: 需要内容长度](https://tools.ietf.org/html/rfc7231#section-6.5.10){data-tooltip="未定义“Content-Length”。服务器在没有它的情况下不会接受请求。"}
- [412: 前提条件失败](https://tools.ietf.org/html/rfc7232#section-4.2){data-tooltip="服务器评估请求中给出的前提条件为 false。"}
- [413: 负载过大](https://tools.ietf.org/html/rfc7231#section-6.5.11){data-tooltip="服务器不会接受该请求，因为请求实体过大。"}
- [414: URI 过长](https://tools.ietf.org/html/rfc7231#section-6.5.12){data-tooltip="服务器不会接受该请求，因为 URL 太长。当您将带有长查询信息的“post”请求转换为“get”请求时发生。"}
- [415: 不支持的媒体类型](https://tools.ietf.org/html/rfc7231#section-6.5.13){data-tooltip="服务器不会接受该请求，因为不支持该媒体类型。"}
- [416: 范围不满足](https://tools.ietf.org/html/rfc7233#section-4.4){data-tooltip="请求的字节范围不可用且超出范围。"}
- [417: 期望失败](https://tools.ietf.org/html/rfc7231#section-6.5.14){data-tooltip="此服务器无法满足 Expect 请求头字段中给出的期望。"}
- [421: 错误导向的请求](https://tools.ietf.org/html/rfc7540#section-9.1.2){data-tooltip="请求被导向到一个无法产生响应的服务器。"}
- [426: 需要升级](https://tools.ietf.org/html/rfc7231#section-6.5.15){data-tooltip="服务器拒绝使用当前协议执行请求，但在客户端升级到不同协议后可能愿意这样做。"}
- [428: 需要前提条件](https://tools.ietf.org/html/rfc6585#section-3){data-tooltip="源服务器要求该请求是附带条件的。"}
- [429: 请求过多](https://tools.ietf.org/html/rfc6585#section-4){data-tooltip="用户在给定时间内发送了太多请求。"}
- [431: 请求头字段太大](https://tools.ietf.org/html/rfc6585#section-5){data-tooltip="服务器不愿意处理该请求，因为其头字段太大。"}
- [451: 因法律原因不可用](https://datatracker.ietf.org/doc/html/rfc7725#section-3){data-tooltip="此状态代码表示服务器因法律要求而拒绝访问资源。"}

### 1xx. 信息性状态码

<!-- prettier-ignore -->
- [100: 继续](https://tools.ietf.org/html/rfc7231#section-6.2.1){data-tooltip="服务器仅收到请求的一部分，但只要请求未被拒绝，客户端就应继续该请求。"}
- [101: 切换协议](https://tools.ietf.org/html/rfc7231#section-6.2.2){data-tooltip="服务器切换协议。"}
- [102: 处理中](https://tools.ietf.org/html/rfc2518#section-10.1){data-tooltip="一个临时响应，用于通知客户端服务器已接受完整请求，但尚未完成。"}
- [103: 早期提示](https://tools.ietf.org/html/rfc8297){data-tooltip="向客户端指示服务器可能发送最终响应，其中包含信息响应中包含的头字段。"}

### 3xx. 重定向状态码

<!-- prettier-ignore -->
- [300: 多种选择](https://tools.ietf.org/html/rfc7231#section-6.4.1){data-tooltip="一个链接列表。用户可以选择一个链接并转到该位置。最多五个地址。"}
- [301: 永久移动](https://tools.ietf.org/html/rfc7231#section-6.4.2){data-tooltip="请求的页面已移至新的 URL。"}
- [302: 找到](https://tools.ietf.org/html/rfc7231#section-6.4.3){data-tooltip="请求的页面已临时移至新的 URL。"}
- [303: 查看其他位置](https://tools.ietf.org/html/rfc7231#section-6.4.4){data-tooltip="可以在不同的 URL 下找到请求的页面。"}
- [304: 未修改](https://tools.ietf.org/html/rfc7232#section-4.1){data-tooltip="这是对 If-Modified-Since 或 If-None-Match 头的响应代码，表示自指定日期以来 URL 未被修改。"}
- [305: 使用代理](https://tools.ietf.org/html/rfc7231#section-6.4.5){data-tooltip="必须通过 Location 头中提到的代理访问请求的 URL。"}
- [306: 未使用](https://tools.ietf.org/html/rfc7231#section-6.4.6){data-tooltip="此代码在先前版本中使用过。现已不再使用，但该代码被保留。"}
- [307: 临时重定向](https://tools.ietf.org/html/rfc7231#section-6.4.7){data-tooltip="请求的页面已临时移至新的 URL。"}
- [308: 永久重定向](https://tools.ietf.org/html/rfc7538#section-3){data-tooltip="该请求及所有将来的请求都应使用另一个 URI 重复。"}

### 5xx. 服务器错误状态码

<!-- prettier-ignore -->
- [500: 内部服务器错误](https://tools.ietf.org/html/rfc7231#section-6.6.1){data-tooltip="请求未完成。服务器遇到意外情况。"}
- [501: 未实现](https://tools.ietf.org/html/rfc7231#section-6.6.2){data-tooltip="请求未完成。服务器不支持所需的功能。"}
- [502: 错误网关](https://tools.ietf.org/html/rfc7231#section-6.6.3){data-tooltip="请求未完成。服务器从上游服务器收到无效响应。"}
- [503: 服务不可用](https://tools.ietf.org/html/rfc7231#section-6.6.4){data-tooltip="请求未完成。服务器暂时过载或宕机。"}
- [504: 网关超时](https://tools.ietf.org/html/rfc7231#section-6.6.5){data-tooltip="网关已超时。"}
- [505: HTTP 版本不受支持](https://tools.ietf.org/html/rfc7231#section-6.6.6){data-tooltip="服务器不支持该“http 协议”版本。"}
- [506: 变体也协商](https://tools.ietf.org/html/rfc2295#section-8.1){data-tooltip="请求的透明内容协商导致循环引用。"}
- [507: 存储空间不足](https://tools.ietf.org/html/rfc4918#section-11.5){data-tooltip="服务器无法存储完成请求所需的表示。"}
- [508: 检测到循环](https://tools.ietf.org/html/rfc5842#section-7.2){data-tooltip="服务器在处理请求时检测到无限循环。"}
- [510: 未扩展](https://tools.ietf.org/html/rfc2774#section-7){data-tooltip="服务器需要对请求进行进一步扩展才能完成它。"}
- [511: 需要网络身份验证](https://tools.ietf.org/html/rfc6585#section-6){data-tooltip="客户端需要进行身份验证才能获得网络访问权限。"}

