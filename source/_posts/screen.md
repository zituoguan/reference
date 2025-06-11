---
title: Screen
date: 2021-01-02 20:03:55
background: bg-emerald-500
tags:
  - 终端
  - 会话
  - 实用工具
categories:
  - Linux 命令
intro: |
  这是 screen 命令的快速参考指南备忘单。
plugins:
  - copyCode
---

## 入门

### 入门

```shell script
$ screen
```

1\. 按 <kbd>Ctrl-A</kbd> <kbd>D</kbd> 分离会话

---

2\. 列出所有 screen 会话

```shell script
$ screen -ls
```

3\. 重新附加一个 screen 会话

```shell script
$ screen -r <名称/PID>
```

### 选项 {.col-span-2}

| 选项   | 示例                                  | 描述                                                    |
| ------ | ------------------------------------- | ------------------------------------------------------- |
| `-S`   | screen -S debug                       | 使用会话名称启动一个新会话                                  |
| `-ls`  | screen -ls                            | 列出正在运行的会话/屏幕                                   |
| `-x`   | screen -x                             | 附加到一个正在运行的会话                                  |
| `-r`   | screen -r debug                       | 通过名称附加到一个正在运行的会话                            |
| `-R`   | screen -R debug                       | 附加到一个会话 _(如果不存在则创建)_                         |
| `-d`   | screen -d -m wget xxxx.com/large.file | 以分离模式启动 screen                                     |
| `-X`   | screen -X -S debug kill               | 终止一个正在运行的会话                                    |

{.show-header}

### 帮助

| 命令         | 描述                       |
| ------------ | -------------------------- |
| `Ctrl-A` `?` | 查看帮助 _(列出快捷键)_      |

{.shortcuts}

### 窗口管理 {.col-span-2 .row-span-2}

| 命令                                   | 描述                                 |
| -------------------------------------- | ------------------------------------ |
| `Ctrl-A` `C`                           | 创建新窗口                           |
| `Ctrl-A` `Ctrl-A`                      | 切换到上一个访问的活动窗口             |
| `Ctrl-A` `0...9`                       | 按编号切换到窗口                     |
| `Ctrl-A` `'` `<0...9 或 标题>`        | 按编号或名称切换到窗口               |
| `Ctrl-A` `N` 或 `Ctrl-A` `<space>`     | 切换到列表中的下一个窗口             |
| `Ctrl-A` `P` 或 `Ctrl-A` `<backspace>` | 切换到列表中的上一个窗口             |
| `Ctrl-A` `"`                           | 查看窗口列表                         |
| `Ctrl-A` `W`                           | 显示窗口栏                           |
| `Ctrl-A` `K`                           | 终止当前窗口 _(不推荐)_              |
| `Ctrl-A` `\`                           | 终止所有窗口 _(不推荐)_              |
| `Ctrl-A` `A`                           | 重命名当前窗口                       |

{.shortcuts}

### 退出

| 命令             | 描述                                  |
| ---------------- | ------------------------------------- |
| `Ctrl-A` `D`     | 分离                                  |
| `Ctrl-A` `D` `D` | 分离并注销 <br>_(快速退出)_            |
| `Ctrl-A` `:`     | 退出所有会话                          |
| `Ctrl-A` `C-\`   | 强制退出 screen <br>_(不推荐)_        |

{.shortcuts}

### 分割屏幕

| 命令           | 描述                                   |
| -------------- | -------------------------------------- |
| `Ctrl-A` `S`   | 水平分割显示                           |
| `Ctrl-A` `V`   | 垂直分割显示                           |
| `Ctrl-A` `     | `                                      | 垂直分割显示                           |
| `Ctrl-A` `TAB` | 跳转到下一个显示区域                   |
| `Ctrl-A` `X`   | 移除当前区域                           |
| `Ctrl-A` `Q`   | 移除除当前区域外的所有区域             |

{.shortcuts}

### 杂项 {.col-span-2 .row-span-2}

| 命令              | 描述                                   |
| ----------------- | -------------------------------------- |
| `Ctrl-A` `C-l`    | 重绘窗口                               |
| `Ctrl-A` `[`      | 进入复制模式                           |
| `Ctrl-A` `ESC`    | 进入复制模式                           |
| `Ctrl-A` `]`      | 粘贴                                   |
| `Ctrl-A` `M`      | 监控窗口活动                           |
| `Ctrl-A` `_`      | 监控窗口静默                           |
| `Ctrl-A` `Ctrl-V` | 输入双字符 <br>_(非 ASCII 字符)_       |
| `Ctrl-A` `X`      | 锁定 (密码保护) 显示                   |
| `Ctrl-A` `:`      | 进入 screen 命令                       |
| `Ctrl-A` `H`      | 在 screen 会话中启用日志记录           |

{.shortcuts}

### Screen 技巧

SSH 并一步附加

```shell script
$ ssh -t user@host screen -x <名称/PID>
```
