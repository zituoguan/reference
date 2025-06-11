---
title: Lsof 命令
date: 2021-02-05 16:12:47
background: bg-blue-400
tags:
  - port
  - processes
  - utility
categories:
  - Linux 命令
intro: |
  本快速参考备忘单提供了 `lsof` 命令的各种用法。
plugins:
  - copyCode
---

## 入门

### 简介

**lsof** 的含义是 `L`i`S`t `O`pen `F`iles（列出打开的文件），用于找出哪些进程打开了哪些文件。

```shell script
$ lsof
$ sudo lsof -u root
```

### 特定端口

```shell script
$ lsof -i :8080
$ lsof -i :80 -i :22
$ lsof -i TCP:22
$ lsof -i TCP:1-1024
$ lsof -i UDP
$ lsof -i @192.168.1.5
```

### 特定进程

```shell script
$ lsof -c mysql
$ lsof -c java
$ lsof -c ssh
$ lsof -c nginx
$ lsof -c ssh -c httpd
```

### 特定用户

```shell script
$ lsof -u www-data
$ lsof -u www-data -u ubuntu
$ lsof -i -u ^root # 排除特定用户
```

### 特定网络

```shell script
$ lsof -i 4   # 仅 IPv4
$ lsof -i 6   # 仅 IPv6
```

### 特定 PID

```shell script
$ lsof -p 1753
$ lsof -p ^3  # 排除特定 PID
```

### 特定文件名

```shell script
$ lsof /var/log/messages
$ lsof /etc/passwd
```

### 特定目录

```shell script
$ lsof +D /var/log # 目录内
```

### 终止进程

```shell script
$ kill -9 `lsof -t -u apache`
$ kill -9 $(lsof -t -i :8080)
```

