---
title: Homebrew
date: 2023-04-12
background: bg-[#fbb041]
tags:
  - 软件包管理器
  - macos
categories:
  - 工具箱
intro: 这是 Homebrew 入门的快速参考备忘单。
plugins:
  - copyCode
---

## 入门指南

### 安装

如果尚未安装，请安装命令行工具 (CLT)

```bash
xcode-select --install
```

安装 Homebrew：

```bash {.wrap}
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

[官方网站](https://brew.sh/) {.link-arrow}

### 命令

|                            |                                        |
| -------------------------- | -------------------------------------- |
| `brew install git`         | 安装一个软件包                      |
| `brew uninstall git`       | 卸载一个软件包                    |
| `brew upgrade git`         | 升级软件包                        |
| `brew unlink git`          | 取消链接                                 |
| `brew link git`            | 链接                                   |
| `brew switch git  1.0.0`   | 切换软件包版本                 |
| `brew list --versions git` | 列出软件包已安装的版本 |

### 帮助

显示 Homebrew 的版本。

```bash
brew --version
```

打印帮助信息

```bash
brew help
```

打印 brew 命令的帮助信息

```bash
brew help <sub-command>
```

检查系统是否存在潜在问题。

```bash
brew doctor
```

### 更新

获取 Homebrew 和配方的最新版本

```bash
brew update
```

显示有可用更新版本的配方

```bash
brew outdated
```

升级所有过时且未固定的 brew

```bash
brew upgrade
```

仅升级指定的 brew

```bash
brew upgrade <formula>
```

阻止指定的配方被升级

```bash
brew pin <formula>
```

允许指定的配方被升级。

```bash
brew unpin <formula>
```

### 仓库

列出所有当前的 tapped 仓库 (taps)

```bash
brew tap
```

从 Github 使用 https tap 一个配方仓库，例如 tap https://github.com/user/homebrew-repo

```bash
brew tap <user/repo>
```

从指定的 URL tap 一个配方仓库

```bash
brew tap <user/repo> <URL>
```

从仓库中移除给定的 tap

```bash
brew untap <user/repo>
```

### Cask

从 Github tap Cask 仓库。

```bash
brew tap homebrew/cask
```

列出所有已安装的 cask。

```bash
brew cask list
```

根据子字符串文本搜索所有已知的 cask。

```bash
brew search <text>
```

安装给定的 cask。

```bash
brew cask install <cask>
```

重新安装给定的 Cask

```bash
brew cask reinstall <cask>
```

卸载给定的 cask。

```bash
brew cask uninstall <cask>
```

### 搜索、安装、移除

列出所有已安装的配方。

```bash
brew list
```

显示所有本地可用于 brewing 的配方。

```bash
brew search
```

对用于 brewing 的配方名称进行子字符串搜索。

```bash
brew search <text>
```

显示关于配方的信息。

```bash
brew info <formula>
```

安装配方。

```bash
brew install <formula>
```

卸载配方。

```bash
brew uninstall <formula>
```

### 清理

移除已安装配方的旧版本。

```bash
brew cleanup
```

移除指定配方的旧版本。

```bash
brew cleanup <formula>
```

显示所有将被移除的配方（试运行）

```bash
brew cleanup -n
```
