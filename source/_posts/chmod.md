---
title: Chmod
date: 2021-07-01 10:51:44
background: bg-emerald-600
tags:
  - 权限
categories:
  - Linux 命令
intro: |
  这份快速参考备忘单简要概述了文件权限以及 chmod 命令的操作。
plugins:
  - copyCode
---

## 入门指南

### 语法

```shell script
$ chmod [选项] <权限> <文件>
```

#### 示例

```shell
$ chmod 755 foo.txt
$ chmod +x cheatsheets.py
$ chmod u-x cheatsheets.py
$ chmod u=rwx,g=rx,o= cheatsheets.sh
```

#### 递归更改文件和目录

```shell
$ chmod -R 755 my_directory
```

`chmod` 命令代表 "change mode" (更改模式)。

### Chmod 生成器

<widget name="chmod"/>

Chmod 生成器允许您以数字和符号形式快速直观地生成权限。

### 常用权限

| 命令  | s         | 含义                         |
| ------- | --------- | ---------------------------- |
| `400`   | r-------- | 仅所有者可读                 |
| `500`   | r-x------ | 避免更改                     |
| `600`   | rw------- | 用户可更改                   |
| `644`   | rw-r--r-- | 用户可读和更改               |
| `660`   | rw-rw---- | 用户和组可更改               |
| `700`   | rwx------ | 仅用户拥有完全访问权限       |
| `755`   | rwxr-xr-x | 仅用户可更改                 |
| `775`   | rwxrwxr-x | 组的共享模式                 |
| `777`   | rwxrwxrwx | 任何人都可以执行任何操作     |

### 说明

```shell
$ ls -l
-rw-r--r--  1 root root 3 Jun 29 15:35 a.log
drwxr-xr-x  2 root root 2 Jun 30 18:06 dir
```

#### "dir" 的权限分析

```text
d  rwx  r-x  r-x
┬  ─┬─  ─┬─  ─┬─
│   │    │    │
│   │    │    └─ 4. 其他人｜5 (4+0+1)
│   │    └────── 3. 组｜5 (4+0+1)
│   └─────────── 2. 用户｜7 (4+2+1)
└─────────────── 1. 文件类型 | 目录
```

### 权限模式 {.col-span-2}

| 权限  | 描述             | 八进制 | 十进制    |
| ---------- | ----------------------- | ----- | --------- |
| `---`      | 无权限           | 000   | 0 (0+0+0) |
| `--x`      | 执行                 | 001   | 1 (0+0+1) |
| `-w-`      | 写入                 | 010   | 2 (0+2+0) |
| `-wx`      | 执行和写入       | 011   | 3 (0+2+1) |
| `r--`      | 读取                 | 100   | 4 (4+0+0) |
| `r-x`      | 读取和执行        | 101   | 5 (4+0+1) |
| `rw-`      | 读取和写入        | 110   | 6 (4+2+0) |
| `rwx`      | 读取、写入和执行 | 111   | 7 (4+2+1) |

{.show-header}

### 对象

| 用户 (缩写) | 含义                       |
| ----------- | -------------------------- |
| `u`         | `U`ser (用户)              |
| `g`         | `G`roup (组)               |
| `o`         | `O`thers (其他人)          |
| `a`         | `A`ll (所有), 等同于 ugo |

{.show-header}

### 权限

| 缩写 | 权限          | 值   |
| ------------ | ------------- | ----- |
| `r`          | `R`ead (读取)   | 4     |
| `w`          | `W`rite (写入)  | 2     |
| `x`          | E`x`ecute (执行)| 1     |
| `-`          | 无权限        | 0     |

{.show-header}

### 文件类型

| 缩写 | 文件类型                |
| ------------ | ----------------------- |
| `d`          | `D`irectory (目录)      |
| `-`          | 普通文件                |
| `l`          | Symbolic `L`ink (符号链接) |

{.show-header}

## Chmod 示例

### 操作符

| 符号 | 描述   |
| ------ | ------ |
| `+`    | 添加   |
| `-`    | 移除   |
| `=`    | 设置   |

### chmod 600

```shell
$ chmod 600 example.txt
$ chmod u=rw,g=,o= example.txt
$ chmod a+rwx,u-x,g-rwx,o-rwx example.txt
```

### chmod 664

```shell
$ chmod 664 example.txt
$ chmod u=rw,g=rw,o=r example.txt
$ chmod a+rwx,u-x,g-x,o-wx example.txt
```

### chmod 777

```shell
$ chmod 777 example.txt
$ chmod u=rwx,g=rwx,o=rwx example.txt
$ chmod a=rwx example.txt
```

### 符号模式 {.row-span-3}

拒绝所有人的执行权限。

```shell
$ chmod a-x chmodExampleFile.txt
```

允许所有人读取权限。

```shell
$ chmod a+r chmodExampleFile.txt
```

使文件对组和其他人可读写。

```shell
$ chmod go+rw chmodExampleFile.txt
```

使 shell 脚本对用户/所有者可执行。

```shell
$ chmod u+x chmodExampleScript.sh
```

允许所有人读、写、执行文件，并开启 set group-ID。

```shell
$ chmod =rwx,g+s chmodExampleScript.sh
```

### 移除权限 {.row-span-3}

要移除授予文件的读写权限，请使用以下语法：

```shell
$ chmod o-rw example.txt
```

对于我们的文件 example.txt，我们可以通过运行以下命令使用 chmod 移除组的读写权限：

```shell
$ chmod  g-rx example.txt
```

要从组中移除 chmod 读写权限，同时为公共/其他人添加读写权限，我们可以使用以下命令：

```shell
$ chmod g-rx, o+rx example.txt
```

但是，如果您希望移除组和其他人的所有权限，可以使用 `go=` 来实现：

```shell
$ chmod go= example.txt
```

### 可执行文件

```shell
$ chmod +x ~/example.py
$ chmod u+x ~/example.py
$ chmod a+x ~/example.py
```

### chmod 754

```shell
$ chmod 754 foo.sh
$ chmod u=rwx,g=rx,o=r foo.sh
```

## Chmod 实践

### SSH 权限

```shell script
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/id_rsa
$ chmod 600 ~/.ssh/id_rsa.pub
$ chmod 400 /path/to/access_key.pem
```

### Web 权限

```shell script
$ chmod -R 644 /var/www/html/
$ chmod 644 .htaccess
$ chmod 644 robots.txt
$ chmod 755 /var/www/uploads/
$ find /var/www/html -type d -exec chmod 755 {} \;
```

### 批量更改

```shell script
$ chmod -R 644 /your_path
$ find /path -type d -exec chmod 755 {} \;
$ find /path -type f -exec chmod 644 {} \;
```

参见：[命令替换](https://tldp.org/LDP/abs/html/commandsub.html)

## 另请参阅

- [使用 chmod 修改文件权限](https://www.linode.com/docs/guides/modify-file-permissions-with-chmod/)
  _(linode.com)_
