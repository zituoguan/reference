---
title: Tmux
date: 2021-02-20 14:31:24
background: bg-emerald-600
tags:
  - 实用工具
  - 终端
  - 会话
categories:
  - Linux 命令
intro: |
  Tmux 快捷键和常用命令速查表。
plugins:
  - copyCode
---

## Tmux 命令行界面

### 新建会话 {.row-span-2}

启动一个新会话

```shell script
$ tmux
```

启动一个命名的新会话

```shell script
$ tmux new -s myname
```

显示所有会话

```shell script
$ tmux ls
```

### 附加会话

附加到上一个会话

```shell script
$ tmux a
```

附加到指定名称的会话

```shell script
$ tmux a -t myname
```

### 终止会话 {.row-span-2}

按名称终止会话

```shell script
$ tmux kill-ses -t myname
```

终止除当前会话外的所有会话

```shell script
$ tmux kill-ses -a
```

终止除 'myname' 会话外的所有会话

```shell script
$ tmux kill-ses -a -t myname
```

### Tmux 帮助

```shell script
$ tmux info
```

### 配置

重新加载配置

```shell script
$ tmux source-file ~/.tmu­x.conf
```

显示配置

```shell script
$ tmux show-options -g
```

### 复制模式

| 命令         | 描述                   |
| ------------ | -------------------------- |
| `Ctrl+b` `[` | 进入复制模式               |
| `<Space>`    | 开始选择                   |
| `Enter`      | 复制选中内容               |
| `q`          | 退出复制模式               |
| `Ctrl+b` `]` | 粘贴缓冲区0的内容          |

-------------
在 MacOS 15.3.1 Sequoia 上的 tmux 3.5a 版本中，“复制模式”的功能略有不同。
下面我写出了不同之处：
| 命令            | 描述                   |
| ------------       | -------------------------- |
| `Ctrl + <Space>`   | 开始选择                   |
| `Ctrl + w`         | 复制选中内容               |

-------------

{.shortcuts}

主要操作方式类似于在 [Vim](/vim#motions) 中选择文本。

## Tmux 快捷键

### 入门 {.secondary}

| 快捷键       | 描述           |
| ------------ | ------------------ |
| `Ctrl+b` `?` | 列出所有快捷键     |

{.shortcuts .show-header}

<br/>

---

显示每个会话、窗口、窗格等。

```shell script
$ tmux info
```

### 窗格 (分割) {.row-span-2}

| 快捷键                 | 描述               |
| ---------------------- | ------------------ |
| `Ctrl+b` `"` _/_ `%`   | 水平/垂直分割      |
| `Ctrl+b` `!`           | 窗格 -> 窗口       |
| `Ctrl+b` `x`           | 关闭窗格           |
| `Ctrl+b` <方向键\>     | 导航窗格           |
| `Ctrl+b` <Space\>      | 切换布局           |
| `Ctrl+b` `{` _/_ `}`   | 移动到左侧/右侧    |
| `Ctrl+b` `o`           | 转到下一个窗格     |
| `Ctrl+b` `z`           | 切换全屏           |
| `Ctrl+b` `;`           | 切换到上一个窗格   |
| `Ctrl+b` `q`           | 显示编号           |
| `Ctrl+b` `q` `0`...`9` | 转到编号 # 的窗格  |

{.shortcuts}

### 窗口 (标签页) {.row-span-2}

| -                    | -                    |
| -------------------- | -------------------- |
| `Ctrl+b` `c`         | 创建窗口             |
| `Ctrl+b` `p` _/_ `n` | 上一个/下一个窗口    |
| `Ctrl+b` `"` _/_ `%` | 水平/垂直分割      |
| `Ctrl+b` `w`         | 列出窗口             |
| `Ctrl+b` `,`         | 重命名窗口           |
| `Ctrl+b` `f`         | 查找窗口             |
| `Ctrl+b` `l`         | 上一个窗口           |
| `Ctrl+b` `.`         | 移动窗口             |
| `Ctrl+b` `&`         | 关闭窗口             |
| `Ctrl+b` `0`...`9`   | 转到编号 # 的窗口    |

{.shortcuts}

### 会话 (窗口集合)

| -                    | -                              |
| -------------------- | ------------------------------ |
| `Ctrl+b` `d`         | <red>从会话中分离</red>        |
| `Ctrl+b` `s`         | 显示所有会话                   |
| `Ctrl+b` `$`         | 重命名会话                     |
| `Ctrl+b` `(` _/_ `)` | 上一个/下一个会话              |

{.shortcuts}

## Tmux 命令模式

### 用法 {.secondary}

| 命令         | 描述           |
| ------------ | ------------------ |
| `Ctrl+b` `:` | 进入命令模式       |

{.shortcuts}

### 调整大小

| 命令                | 描述     |
| ------------------- | ------------ |
| `resize-pane -D 20` | 向下调整大小 |
| `resize-pane -U 20` | 向上调整大小 |
| `resize-pane -L 20` |向左调整大小 |
| `resize-pane -R 20` |向右调整大小 |

### 列表

| 命令           | 描述     |
| -------------- | ------------ |
| `list-keys`    | 所有命令   |
| `list-panes`   | 所有窗格   |
| `list-windows` | 所有窗口   |

### 复制

| 命令                 | 描述         |
| -------------------- | ---------------- |
| `list-buffers`       | 列出所有缓冲区   |
| `show-buffer`        | 显示 #0 的内容   |
| `capture-pane`       | 复制窗格内容     |
| `choose-buffer`      | 显示并粘贴       |
| `save-buffer a.txt`  | 保存到文件       |
| `delete-buffer -b 1` | 删除缓冲区 1     |

### 设置

| 命令                   | 描述             |
| ---------------------- | -------------------- |
| `set -g OPTION`        | 为所有会话设置       |
| `setw -g OPTION`       | 为所有窗口设置       |
| `setw -g mode-keys vi` | 启用 vi 模式         |
| `set -g prefix C-a`    | 设置前缀             |

### 杂项

| 命令                     | 描述         |
| ------------------------ | ------------ |
| `swap-pane -s 3 -t 1`    | 交换窗格     |
| `swap-window -t -1`      | 向左移动窗口 |
| `setw synchronize-panes` | 同步窗格     |
| `join-pane -t :#`        | 合并窗格     |

