---
title: SSH
date: 2021-01-27 11:48:05
background: bg-blue-400
tags:
  - protocol
  - remote
  - network
  - 22
categories:
  - Linux 命令
intro: |
  本快速参考备忘单提供了各种使用 SSH 的方法。
plugins:
  - copyCode
---

## 入门指南

### 连接

连接到服务器（默认端口 22）

```shell script
$ ssh root@192.168.1.5
```

通过指定端口连接

```shell script
$ ssh root@192.168.1.5 -p 6222
```

通过 pem 文件连接（0400 权限）

```shell script
$ ssh -i /path/file.pem root@192.168.1.5
```

参见：[SSH 权限](/chmod#ssh-permissions)

### 执行命令

执行远程命令

```shell script
$ ssh root@192.168.1.5 'ls -l'
```

调用本地脚本

```shell script
$ ssh root@192.168.1.5 bash < script.sh
```

压缩并从服务器下载

```shell script {.wrap}
$ ssh root@192.168.1.5 "tar cvzf - ~/source" > output.tgz
```

### SCP {.row-span-2}

从远程复制到本地

```shell script
$ scp user@server:/dir/file.ext dest/
```

在两台服务器之间复制

```shell script
$ scp user@server:/file user@server:/dir
```

从本地复制到远程

```shell script
$ scp dest/file.ext user@server:/dir
```

复制整个文件夹

```shell script
$ scp -r user@server:/dir dest/
```

复制文件夹中的所有文件

```shell script
$ scp user@server:/dir/* dest/
```

从服务器文件夹复制到当前文件夹

```shell script
$ scp user@server:/dir/* .
```

### 配置文件位置

| 文件路径                 | 描述                 |
| ------------------------ | -------------------- |
| `/etc/ssh/ssh_config`    | 系统范围配置         |
| `~/.ssh/config`          | 用户特定配置         |
| `~/.ssh/id_{type}`       | 私钥                 |
| `~/.ssh/id_{type}.pub`   | 公钥                 |
| `~/.ssh/known_hosts`     | 已知主机             |
| `~/.ssh/authorized_keys` | 授权登录密钥         |

### SCP 选项

| 选项          | 描述                                   |
| ------------- | ---------------------------------------------- |
| scp `-r`      | <yel>R</yel>ecursively 递归复制整个目录       |
| scp `-C`      | <yel>C</yel>ompresses 压缩数据                 |
| scp `-v`      | Prints <yel>v</yel>erbose 打印详细信息        |
| scp `-P` 8080 | Uses a specific <yel>P</yel>ort 使用指定端口   |
| scp `-B`      | <yel>B</yel>atch mode 批处理模式 _(阻止密码提示)_ |
| scp `-p`      | <yel>P</yel>reserves 保留时间和模式           |

### 配置示例

```toml
Host server1
    HostName 192.168.1.5
    User root
    Port 22
    IdentityFile ~/.ssh/server1.key
```

通过别名启动

```shell script
$ ssh server1
```

参见：完整的 [配置选项](https://linux.die.net/man/5/ssh_config)

### ProxyJump (代理跳转)

```shell script
$ ssh -J proxy_host1 remote_host2
```

```shell script {.wrap}
$ ssh -J user@proxy_host1 user@remote_host2
```

多次跳转

```shell script {.wrap}
$ ssh -J user@proxy_host1:port1,user@proxy_host2:port2 user@remote_host3
```

### ssh-copy-id

```shell script {.wrap}
$ ssh-copy-id user@server
```

复制到别名服务器

```shell script {.wrap}
$ ssh-copy-id server1
```

复制特定密钥

```shell script {.wrap}
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```

## SSH 密钥生成 {.cols-5}

### ssh-keygen {.col-span-2}

```shell script
$ ssh-keygen -t rsa -b 4096 -C "your@mail.com"
```

---

| -   | -    | -                             |
| --- | ---- | ----------------------------- |
|     | `-t` | 密钥[类型](#key-type)         |
|     | `-b` | 密钥中的位数                  |
|     | `-C` | 提供新注释                    |

{.left-text}

生成一个 RSA 4096 位密钥，并以电子邮件作为注释

### 生成 {.col-span-2 .row-span-2}

交互式生成密钥

```shell script
$ ssh-keygen
```

指定文件名

```shell script
$ ssh-keygen -f ~/.ssh/filename
```

从私钥生成公钥

```shell script
$ ssh-keygen -y -f private.key > public.pub
```

更改注释

```shell script
$ ssh-keygen -c -f ~/.ssh/id_rsa
```

更改私钥密码

```shell script
$ ssh-keygen -p -f ~/.ssh/id_rsa
```

### 密钥类型

- rsa
- ed25519
- dsa
- ecdsa

### known_hosts {.col-span-2}

从 known_hosts 搜索

```shell script
$ ssh-keygen -F <ip/hostname>
```

从 known_hosts 删除

```shell script
$ ssh-keygen -R <ip/hostname>
```

### 密钥格式

- PEM
- PKCS8

## 另请参阅

- [OpenSSH 配置文件示例](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/) _(cyberciti.biz)_
- [ssh_config](https://linux.die.net/man/5/ssh_config) _(linux.die.net)_
