---
title: Netstat
date: 2021-01-27 11:44:21
background: bg-slate-700
tags:
  - 网络
  - 实用工具
  - 端口
categories:
  - Linux 命令
intro: |
  本快速参考备忘单提供了 netstat 命令的各种用法。
plugins:
  - copyCode
---

## 入门

### 统计信息

端口 80 上的所有连接

```shell script
$ netstat -anp | grep :80
```

Netstat 帮助

```shell script
$ netstat -h
```

### 监听端口

| 选项             | 示例                 |
| ---------------- | -------------------- |
| `netstat -ltunp` | 所有监听端口         |
| `netstat -ltn`   | 监听 TCP 端口        |
| `netstat -lun`   | 监听 UDP 端口        |
| `netstat -lx`    | 监听 Unix 端口       |

### 连接

| 选项          | 示例               |
| ------------- | ------------------- |
| `netstat -a`  | 所有连接           |
| `netstat -at` | 所有 TCP 连接      |
| `netstat -au` | 所有 UDP 连接      |

### 统计信息

| 选项          | 示例                   |
| ------------- | ---------------------- |
| `netstat -s`  | 显示统计信息           |
| `netstat -st` | 显示 TCP 统计信息      |
| `netstat -su` | 显示 UDP 统计信息      |

### 网络接口

| 选项          | 示例                               |
| ------------- | ------------------------------------- |
| `netstat -i`  | 显示网络接口                         |
| `netstat -ie` | 显示网络接口扩展信息                 |

### 路由

| 选项          | 示例                                   |
| ------------- | --------------------------------------- |
| `netstat -r`  | 显示路由表                             |
| `netstat -rn` | 显示路由表，不解析主机名               |

