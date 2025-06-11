---
title: Alan AI
date: 2023-03-03 6:00:00
background: bg-[#4aa181]
tags:
  - AI
  - AlanAI
  - 提示
  - 技巧
categories:
  - 工具箱
intro:
  此速查表涵盖了所有主要脚本概念、客户端 API 方法、处理程序以及其他工具，用于通过 Alan AI 创建多模式对话体验。
---

### 图例

- `pattern` — 用于调用语音/文本命令或播放响应的短语
- `value` — 指定的值
- `params` — 传递的参数
- `action` — 要执行的操作
- `output` — 数据结果
- `[...]` — 可选数据或参数

## 对话脚本

### 意图和模式

定义一个语音/文本命令以播放响应

```{.wrap}
intent('pattern'[, 'patternN'], reply('pattern'))
```

定义一个语音/文本命令以播放响应或执行操作

```{.wrap}
intent('pattern'[, 'patternN'], p => { action })
```

定义替代方案

```{.wrap}
intent('phrase1|phrase2')
```

定义可选词语和短语

```{.wrap}
intent('pattern (optional phrase|)')
```

### 响应函数

播放响应（如果存在多个模式，则随机选择一个响应）

```{.wrap}
reply('pattern'[, 'patternN'])
```

播放响应

```{.wrap}
p.play('pattern')
```

定义助手回复的语音设置：`口音 (en, fr, de, it, ru, es)`、`性别 (male/female)`、`语音类型`、`语调`、`语速`

```{.wrap}
p.play([voice(code, gender, type, pitch, rate), ]'pattern')
```

定义播放选项：`force:true`（如果按钮未激活则执行），`activate:true`（之前激活按钮），`deactivate:true`（之后停用按钮）

```{.wrap}
p.play('pattern'[, opts(options)])
```

向应用程序发送命令

```{.wrap}
p.play({command:data})
```

### 用户定义的槽位

定义输入中预期的静态值列表

```{.wrap}
$(SLOTNAME value1|value2) => p.SLOTNAME.value
```

提供标签以分类或识别槽位值

```{.wrap}
$(SLOTNAME value1~label1|value2~label2) => p.SLOTNAME.label
```

启用模糊匹配以捕获相似变体

```{.wrap}
$(SLOTNAME~ value1|value2) => p.SLOTNAME.value
```

使槽位可选

```{.wrap}
$(SLOTNAME value1|value2|)
```

捕获多个槽位值

```{.wrap}
intent('$(SLOTNAME value1|value2) and $(SLOTNAME value1|value2 )') => p.SLOTNAME_ (array), p.SLOTNAME_[0].value, p.SLOTNAME_[1].value
```

### 预定义槽位

捕获日期值

```{.wrap}
$(DATE) => p.DATE.value, p.DATE.moment, p.DATE.luxon
```

捕获时间值

```{.wrap}
$(TIME) => p.TIME.value, p.TIME.moment
```

捕获基数

```{.wrap}
$(NUMBER) => p.NUMBER.value, p.NUMBER.number
```

捕获序数

```{.wrap}
$(ORDINAL) => p.ORDINAL.value, p.ORDINAL.number
```

捕获位置

```{.wrap}
$(LOC) => p.LOC.value
```

捕获名称

```{.wrap}
$(NAME) => p.NAME.value
```

### 动态槽位

在项目级别定义动态槽位

```{.wrap}
project.name = {en: "value1|value2|value3"}
$(SLOTNAME p:name) => p.SLOTNAME.value
```

在对话会话级别定义动态槽位

```{.wrap}
p.userData.name = {en: "value1|value2|value3"}
$(SLOTNAME u:name) => p.SLOTNAME.value
```

使用可视化状态获取动态槽位的数据

```{.wrap}
let name = ["value1|value2|value3"]
p.visual.data = {en: name};
$(SLOTNAME v:name) => p.SLOTNAME.value
```

以简短形式定义动态槽位

```{.wrap}
project.name = {en: "value1|value2|value3"}
$(p:name) => p.SLOTNAME.value
```

定义动态槽位的标签：参见[用户定义的槽位](#user-defined-slots)。

为动态槽位启用模糊匹配：参见[用户定义的槽位](#user-defined-slots)。

使动态槽位可选：参见[用户定义的槽位](#user-defined-slots)。

捕获多个槽位值：参见[用户定义的槽位](#user-defined-slots)。

### 正则表达式槽位

捕获数字和/或字母组合

```{.wrap}
const reg = "([A-Za-z]{1}\\s?){6}"
$(SLOTNAME* ${reg}) => p.SLOTNAME.value
```

捕获任何用户输入

```{.wrap}
$(SLOTNAME* .+) => p.SLOTNAME.value
```

### 上下文

定义上下文

```{.wrap}
let contextName = context(() => { action })
```

激活上下文

```{.wrap}
intent('pattern', p => {..., p.then(contextName)}
```

将数据传递到上下文

```{.wrap}
p.then(contextName, state: {data:yourData}) => p.state.data
```

解析上下文

```{.wrap}
p.resolve([data:yourData])
```

重置上下文

```{.wrap}
p.resetContext()
```

定义在任何时候都可匹配的意图，而无需切换当前上下文

```{.wrap}
intent(noctx, 'pattern', ...) or noContext(() => {intent(...)})
```

为预期输入播放提示

```{.wrap}
fallback('pattern1'[, 'patternN'])
```

为上下文命名

```{.wrap}
title('contextName')
```

### 预定义对象

存储从客户端应用程序传递的静态设备和用户特定数据

```{.wrap}
authData.data => p.authData.data
```

存储在项目范围内全局可用的状态数据

```{.wrap}
project.info = {data:yourData} => project.info.data
```

存储意图匹配分数

```{.wrap}
p.score
```

存储在上下文之间传递的数据

```{.wrap}
p.state.data
```

存储通过 `setVisualState()` 从客户端应用程序传递的可视化上下文数据

```{.wrap}
p.visual.data
```

存储在对话会话期间可访问的用户特定状态数据

```{.wrap}
p.userData.data
```

### 预定义回调

定义在脚本保存和对话模型构建时要执行的操作

```{.wrap}
onCreateProject(() => { action })
```

定义在对话会话开始时要执行的操作

```{.wrap}
onCreateUser((p) => { action })
```

定义在对话会话结束时要执行的操作

```{.wrap}
onCleanupUser((p) => { action })
```

定义在设置可视化状态时要执行的操作

```{.wrap}
onVisualState((p, s) => { action })
```

定义在客户端应用程序中触发用户事件时要执行的操作：`buttonReady`、`buttonClicked`、`micPermissionPrompt`、`micAllowed`、`firstActivate`、`showPopup`、`popupCloseClicked`、`recognized`

```{.wrap}
onUserEvent((p, e) => { action })
```

定义在上下文激活时要执行的操作

```{.wrap}
onEnter((p) => { action })
```

### 问答服务

定义要索引的资源的 URL

```{.wrap}
corpus({url: url, depth: depthLevel})
```

定义助手在对话中使用的文本语料库

```{.wrap}
corpus('text')
```

### 内置 JS 库

进行 API 调用

```{.wrap}
axios, request
```

处理时间

```{.wrap}
moment-timezone, luxon
```

处理数组、数字、对象、字符串等

```{.wrap}
lodash
```

### 其他

提供提示列表以帮助识别特定术语

```{.wrap}
recognitionHints('hint'[, 'hintN'])
```

将信息消息写入 Alan Studio 日志

```{.wrap}
console.log(data)
```

将错误消息写入 Alan Studio 日志

```{.wrap}
console.error(data)
```

## 客户端 SDK

### 客户端 API 方法

从客户端应用程序向对话脚本发送有关可视化状态的信息

```{.wrap}
setVisualState(visualStateData:object)
```

无需语音/文本命令即可发送数据或执行操作

```{.wrap}
projectAPI.method = function(p, param, callback) {
  p.userData.data = param.data;
  callback();
};

callProjectApi(method:string, data:object, callback:function)
```

在客户端应用程序中播放文本消息

```{.wrap}
playText(text:string)
```

将文本消息作为用户输入发送给 Alan

```{.wrap}
sendText(text:string)
```

在客户端应用程序中执行命令

```{.wrap}
playCommand(command:object)
```

### 客户端 API 方法 (续)

以编程方式激活 Alan 按钮

```{.wrap}
activate()
```

以编程方式停用 Alan 按钮

```{.wrap}
deactivate()
```

检查 Alan 按钮状态

```{.wrap}
isActive()
```

从父元素、页面中移除 Alan 按钮（在 Web、Ionic 上受支持）

```{.wrap}
remove()
```

检查唤醒词的状态（在 iOS、Android 上受支持）

```{.wrap}
getWakewordEnabled()
```

设置唤醒词的状态（在 iOS、Android 上受支持）

```{.wrap}
setWakewordEnabled(enabled:boolean)
```

### 处理程序

// 示例针对 Web 平台提供

处理从对话脚本发送到客户端应用程序的命令

```{.wrap}
onCommand: function (commandData) { action }
```

处理 Alan 按钮状态更改

```{.wrap}
onButtonState: function (e) { action }
```

处理与 Alan Cloud 中虚拟助手项目的连接状态

```{.wrap}
onConnectionStatus: function (e) { action }
```

处理从 Alan 收到的事件

```{.wrap}
onEvent: function (e) { action }
```

## 另请参阅

- [Alan AI 网站](https://alan.app)
- [关于 Alan 平台](https://alan.app/platform)
- [Alan AI 文档](https://alan.app/docs)

