---
title: PM2
date: 2022-11-25 18:10:00
background: bg-[#230769]
tags:
  - process
categories:
  - Linux 命令
intro: |
  [PM2] 是一个守护进程管理器，可以帮助您管理并保持应用程序在线。PM2 的入门非常简单，它提供了一个简单直观的命令行界面（CLI）。
plugins:
  - copyCode
---

## 入门指南

### 安装

最新的 PM2 版本可以通过 NPM 或 Yarn 安装：

```shell script
$ npm install pm2@latest -g
```

或者

```shell script
$ yarn global add pm2
```

### 启动应用

启动、守护和监控应用程序的最简单方法是使用以下命令行：

```shell script
$ pm2 start app.js
```

或者轻松启动任何其他应用程序：

```shell script
$ pm2 start bashscript.sh
$ pm2 start python-app.py --watch
$ pm2 start binary-file -- --port 1520
```

### 一些可以传递给 CLI 的选项 {.row-span-3}

指定应用名称

```shell script
--name <app_name>
```

当文件更改时监视并重启应用

```shell script
--watch
```

设置应用重载的内存阈值

```shell script
--max-memory-restart <200MB>
```

指定日志文件

```shell script
--log <log_path>
```

向脚本传递额外参数

```shell script
-- arg1 arg2 arg3
```

自动重启之间的延迟时间

```shell script
--restart-delay <delay in ms>
```

日志以时间为前缀

```shell script
--time
```

不自动重启应用

```shell script
--no-autorestart
```

指定 cron 表达式以强制重启

```shell script
--cron <cron_pattern>
```

附加到应用程序日志

```shell script
--no-daemon
```

### 管理进程

管理应用程序状态很简单，以下是相关命令：

```shell script
$ pm2 restart app_name
$ pm2 reload app_name
$ pm2 stop app_name
$ pm2 delete app_name
```

#### 除了 app_name，你还可以传递：

- `all` 对所有进程执行操作
- `id` 对特定的进程 ID 执行操作

### 查看状态、日志、指标 {.row-span-2}

启动应用程序后，您可以查看其状态、日志、指标，甚至可以通过 [pm2.io](https://pm2.io/) 获取在线仪表板。

列出 PM2 管理的所有应用程序的状态：

```shell script
$ pm2 [list|ls|status]
```

实时显示日志：

```shell script
$ pm2 logs
```

查看旧日志：

```shell script
$ pm2 logs --lines 200
```

这是一个直接在终端中显示的实时仪表板：

```shell script
$ pm2 monit
```

基于 Web 的仪表板，跨服务器，带诊断系统：

```shell script
$ pm2 plus
```

### 集群模式

对于 Node.js 应用程序，PM2 包含一个自动负载均衡器，它将在每个衍生的进程之间共享所有 HTTP[s]/Websocket/TCP/UDP 连接。

以集群模式启动应用程序：

```shell script
$ pm2 start app.js -i max
```

在此处阅读更多关于集群模式的信息：[链接](https://pm2.keymetrics.io/docs/usage/quick-start/)。

### Ecosystem 文件 {.row-span-2}

您还可以创建一个名为 Ecosystem 文件的配置文件来管理多个应用程序。要生成 Ecosystem 文件：

```shell script
$ pm2 ecosystem
```

这将生成一个 `ecosystem.config.js` 文件：

```javascript
module.exports = {
  apps : [{
    name: "app",
    script: "./app.js",
    env: {
      NODE_ENV: "development",
    },
    env_production: {
      NODE_ENV: "production",
    }
  }, {
     name: 'worker',
     script: 'worker.js'
  }]
}
```

并轻松启动它：

```shell script
$ pm2 start ecosystem.config.js
```

在此处阅读更多关于应用程序声明的信息：[链接](https://pm2.keymetrics.io/docs/usage/application-declaration/)

### 设置启动脚本

在服务器启动/重启时，使用您管理的进程重启 PM2 至关重要。要解决此问题，只需运行此命令以生成活动的启动脚本：

```shell script
$ pm2 save
```

在此处阅读更多关于启动脚本生成器的信息：[链接](https://pm2.keymetrics.io/docs/usage/startup/)

### 文件更改时重启应用程序

使用 `--watch` 选项非常简单：

```shell
$ cd /path/to/my/app
$ pm2 start env.js --watch --ignore-watch="node_modules"
```

这将监视当前目录及其所有子文件夹中的任何文件更改并重启应用程序，同时忽略 `node_modules` 文件夹中的任何更改 `--ignore-watch="node_modules"`。

然后，您可以使用 `pm2 logs` 查看重启的应用程序日志。

---

### 速查表 {.row-span-2 .col-span-2}

以下是一些值得了解的命令。只需使用示例应用程序或您开发机器上的当前 Web 应用程序尝试它们。

Fork 模式

```shell script
$ pm2 start app.js --name my-api # 命名进程
```

集群模式

```shell script
$ pm2 start app.js -i 0        # 将根据可用 CPU 启动最大数量的带负载均衡的进程
$ pm2 start app.js -i max      # 与上面相同，但已弃用。
$ pm2 scale app +3             # 将 `app` 扩展 3 个 worker
$ pm2 scale app 2              # 将 `app` 扩展或缩减到总共 2 个 worker
```

列表

```shell script
$ pm2 list               # 显示所有进程状态
$ pm2 jlist              # 以原始 JSON 格式打印进程列表
$ pm2 prettylist         # 以美化 JSON 格式打印进程列表

$ pm2 describe 0         # 显示有关特定进程的所有信息

$ pm2 monit              # 监控所有进程
```

日志

```shell script
$ pm2 logs [--raw]       # 以流式传输方式显示所有进程日志
$ pm2 flush              # 清空所有日志文件
$ pm2 reloadLogs         # 重新加载所有日志
```

操作

```shell script
$ pm2 stop all           # 停止所有进程
$ pm2 restart all        # 重启所有进程

$ pm2 reload all         # 将实现零停机时间重载（适用于网络应用程序）

$ pm2 stop 0             # 停止特定进程 ID
$ pm2 restart 0          # 重启特定进程 ID

$ pm2 delete 0           # 将从 pm2 列表中删除进程
$ pm2 delete all         # 将从 pm2 列表中删除所有进程
```

其他

```shell script
$ pm2 reset <process>    # 重置元数据（重启时间等）
$ pm2 updatePM2          # 更新内存中的 pm2
$ pm2 ping               # 确保 pm2 守护进程已启动
$ pm2 sendSignal SIGUSR2 my-app # 向脚本发送系统信号
$ pm2 start app.js --no-daemon
$ pm2 start app.js --no-vizion
$ pm2 start app.js --no-autorestart
```

### 更新 PM2

我们简化了它，版本之间没有重大更改，过程简单明了：

```shell script
$ npm install pm2@latest -g
```

然后更新内存中的 PM2：

```shell script
$ pm2 update
```

## 另请参阅

- [快速入门](https://pm2.keymetrics.io/docs/usage/quick-start/) _(pm2.keymetrics.io)_
