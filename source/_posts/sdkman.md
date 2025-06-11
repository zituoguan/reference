---
title: SDKMAN!
date: 2023-12-18 20:25:30
background: bg-[#cf5e3c]
label:
tags:
  - command
  - 软件开发工具包
  - sdk
categories:
  - Linux 命令
intro: |
  本速查表提供了最常用的 SDKMAN! 命令行指令。
plugins:
  - copyCode
---

## 入门 {.cols-2}

### 安装 SDKMAN!

下载 SDKMAN!

```shell script
$ curl -s "https://get.sdkman.io" | bash
```

安装 SDKMAN!

```shell script
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

检查版本

```shell script
$ sdk version
```

更新

```shell script
$ sdk update
```

帮助

```shell script
$ sdk help
```

### 安装和管理候选版本 {.row-span-2}

列出所有候选版本

```shell script
$ sdk list
```

列出某个候选版本的所有版本

```shell script
$ sdk list <candidate>
```

安装最新版本的候选软件

```shell script
$ sdk install <candidate>
```

安装特定版本的候选软件

```shell script
$ sdk install <candidate> <version>
```

临时切换版本

```shell script
$ sdk use <candidate> <version>
```

永久切换到某个版本

```shell script
$ sdk default <candidate> <version>
```

显示正在使用的特定候选软件版本

```shell script
$ sdk current <candidate>
```

显示所有正在使用的候选软件版本

```shell script
$ sdk current
```

移除某个候选软件版本

```shell script
$ sdk uninstall <candidate> <version>
```

