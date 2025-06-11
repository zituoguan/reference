---
title: Github CLI
date: 2023-11-29
icon:
background: bg-[#808080]
tags:
  - Github
  - CICD
  - CLI
categories:
  - 工具箱
intro: Github CLI 快速参考，一个开源命令行工具，让您可以在终端上使用 GitHub。
plugins:
  - copyCode
---

## 入门指南

### 安装

**Windows**

| 工具   | 安装                             | 升级                             |
| :----- | :------------------------------- | :------------------------------- |
| WinGet | `winget install --id Github.cli` | `winget upgrade --id GitHub.cli` |
| Scoop  | `scoop install gh`               | `scoop update gh`                |
| Choco  | `choco install gh`               | `choco upgrade gh`               |

{.show-header}

**Mac OS**

| 工具     | 安装                | 升级                                        |
| :------- | :--------------------- | :--------------------------------------------- |
| Brew     | `brew install gh`      | `brew upgrade gh`                              |
| MacPorts | `sudo port install gh` | `sudo port selfupdate && sudo port upgrade gh` |

{.show-header}

**Linux**

有关其他 Linux 发行版的安装说明，请参阅[安装说明](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)。

安装脚本：

```bash
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```

---

### 基本用法

**帮助和文档**

显示命令选项：

| 命令             | 描述                                                                 |
| :------------------ | :------------------------------------------------------------------------------------------------------------- |
| `gh help [command]` | Help 为应用程序中的任何命令提供帮助。只需键入 `gh help [命令路径]` 即可获取完整详细信息。 |

**认证**

| 命令             | 描述                                                       |
| :------------------ | :---------------------------------------------------------------- |
| `gh auth login`     | 使用基于 Web 浏览器的默认身份验证                     |
| `gh auth logout`    | 删除主机的身份验证配置               |
| `gh auth refresh`   | 扩展或修复存储凭据的权限范围        |
| `gh auth setup-git` | 配置 git 以使用 GitHub CLI 作为凭据帮助程序           |
| `gh auth status`    | 验证并显示有关您的身份验证状态的信息 |
| `gh auth token`     | 打印 gh 配置为使用的身份验证令牌                      |

使用 Github 令牌：

```shell
$ gh auth --with-token < token.txt
```

### 仓库管理

**通用**

| 命令                 | 描述                                       |
| :---------------------- | :------------------------------------------------ |
| `gh repo create`        | 创建一个新的 GitHub 仓库                    |
| `gh repo list [target]` | 列出用户或组织拥有的仓库 |

**目标**

| 命令                      | 描述                                                    |
| :--------------------------- | :------------------------------------------------------------- |
| `gh repo archive [repo]`     | 归档一个 GitHub 仓库                                    |
| `gh repo clone [dir]`        | 在本地克隆一个 GitHub 仓库                              |
| `gh repo delete [repo]`      | 删除一个 GitHub 仓库                                     |
| `gh repo deploy-key`         | 管理仓库中的部署密钥                             |
| `gh repo edit [repo]`        | 编辑仓库设置                                       |
| `gh repo fork [repo]`        | 创建一个仓库的分支                                  |
| `gh repo rename [name]`      | 重命名一个 GitHub 仓库                                     |
| `gh repo set-default [repo]` | 此命令设置默认远程仓库                |
| `gh repo sync [dest-repo]`   | 从源仓库同步目标仓库             |
| `gh repo view [repo]`        | 显示 GitHub 仓库的描述和 README。 |

### Issues

**搜索 Issues**

| 命令                    | 描述                 |
| :------------------------- | :-------------------------- |
| `gh search issues [query]` | 在 GitHub 上搜索 Issues |

**示例**

```bash
# 搜索匹配关键词 "readme" 和 "typo" 的 issues
$ gh search issues readme typo

# 搜索匹配短语 "broken feature" 的 issues
$ gh search issues "broken feature"

# 在 cli 组织中搜索 issues 和 pull requests
$ gh search issues --include-prs --owner=cli

# 搜索分配给您自己的打开的 issues
$ gh search issues --assignee=@me --state=open

# 搜索评论数量众多的 issues
$ gh search issues --comments=">100"

# 搜索没有标签 "bug" 的 issues
$ gh search issues -- -label:bug
```

### Pull Requests

**Pull Request 操作**

| 命令        | 描述                               |
| :------------- | :---------------------------------------- |
| `gh pr create` | 在 GitHub 上创建一个 Pull Request           |
| `gh pr list`   | 列出 GitHub 仓库中的 Pull Request |
| `gh pr status` | 显示相关 Pull Request 的状态     |

**示例**

```shell
$ gh pr status
```

示例输出：

```
Current branch
  #12 Remove the test feature [user:patch-2]
   - All checks failing - Review required

Created by you
  You have no open pull requests

Requesting a code review from you
  #13 Fix tests [branch]
  - 3/4 checks failing - Review required
  #15 New feature [branch]
   - Checks passing - Approved
```

### Github Actions

**通用操作**

| 命令               | 描述                                                                         |
| :-------------------- | :---------------------------------------------------------------------------------- |
| `gh workflow disable` | 禁用工作流，阻止其运行或在列出工作流时显示 |
| `gh workflow enable`  | 启用工作流，允许其运行并在列出工作流时显示         |
| `gh workflow list`    | 列出工作流文件，默认隐藏禁用的工作流                           |
| `gh workflow run`     | 为给定的工作流创建 workflow_dispatch 事件                               |
| `gh workflow view`    | 查看工作流的摘要                                                      |

**运行操作**

| 命令           | 描述                                                         |
| :---------------- | :------------------------------------------------------------------ |
| `gh run cancel`   | 取消工作流运行                                               |
| `gh run delete`   | 删除工作流运行                                               |
| `gh run download` | 下载由 GitHub Actions 工作流运行生成的构件       |
| `gh run list`     | 列出最近的工作流运行                                           |
| `gh run rerun`    | 重新运行整个运行、仅失败的作业或运行中的特定作业 |
| `gh run view`     | 查看工作流运行的摘要                                    |
| `gh run watch`    | 观察运行直到完成，显示其进度                |

### 别名

**通用别名设置**

| 命令           | 描述                                                      |
| :---------------- | :--------------------------------------------------------------- |
| `gh alias delete` | 删除已设置的别名                                               |
| `gh alias import` | 从 YAML 文件的内容导入别名                  |
| `gh alias list`   | 打印出 gh 配置使用的所有别名            |
| `gh alias set`    | 定义一个在调用时将扩展为完整 gh 命令的词 |

### Releases

**通用操作**

| 命令             | 描述                                  |
| :------------------ | :------------------------------------------- |
| `gh release create` | 为仓库创建一个新的 GitHub Release |
| `gh release list`   | 列出仓库中的 Release                |

**目标命令**

| 命令                   | 描述                             |
| :------------------------ | :-------------------------------------- |
| `gh release delete`       | 删除一个 Release                        |
| `gh release delete-asset` | 从 Release 中删除一个资产          |
| `gh release download`     | 从 GitHub Release 下载资产   |
| `gh release edit`         | 编辑一个 Release                          |
| `gh release upload`       | 将资产文件上传到 GitHub Release  |
| `gh release view`         | 查看有关 GitHub Release 的信息 |

### 配置

**目标设置**

| 命令                 | 描述                                         |
| :---------------------- | :-------------------------------------------------- |
| `gh config clear-cache` | 清除 cli 缓存                                 |
| `gh config get`         | 打印给定配置键的值        |
| `gh config list`        | 打印配置键和值的列表       |
| `gh config set`         | 使用给定键的值更新配置 |

