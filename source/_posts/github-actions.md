---
title: GitHub Actions
date: 2023-11-28
icon:
background: bg-[#808080]
tags:
  - Github
  - CICD
categories:
  - 工具箱
intro:
  GitHub Actions 快速参考，用于自动化软件工作流程，允许开发人员直接从其 GitHub 仓库构建、测试和部署代码。
plugins:
  - copyCode
---

## 入门指南

### 简介

[GitHub Actions](https://docs.github.com/en/actions) 是一个 CI/CD 平台，可实现软件工作流程的自动化，
允许开发人员直接从其 GitHub 仓库构建、测试和部署代码。

---

### 工作流程文件

GitHub Action 工作流程在特殊的 YAML 文件中定义，通常存储在 GitHub 仓库的
`.github/workflows` 目录中。

```yaml
name: hello-world
on: push
jobs:
  hello-world-job:
    runs-on: ubuntu-latest
    steps:
      - name: 你好世界
        run: echo "你好，世界！"
```

**查看工作流程运行情况**

- 在 GitHub.com 上，导航到仓库的主页。
- 在您的仓库名称下，点击 `Actions`。
- 在左侧边栏中，点击您想要显示的工作流程，本例中为 "hello-world"。

---

### 工作流程语法

```yaml
name: learn-github-actions
run-name: ${{ github.actor }} 正在学习 GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
        with:
          node-version: "14"
      - run: npm install -g bats
      - run: bats -v
```

### 工作流程语法说明

| 行                    | 说明                                                                                                                                                              |
| :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name:`               | 设置 GitHub Actions 工作流程的名称。它是在仓库中识别工作流程的标签。                                                                                                   |
| `run-name:`           | 为运行设置自定义名称，使用 GitHub 上下文 `${{ github.actor }}` 来包含发起运行的用户的名称。                                                                                |
| `on:`                 | 指定触发工作流程的事件。在本例中，工作流程由仓库的任何 `push` 事件触发。                                                                                                 |
| `jobs:`               | 定义将作为工作流程一部分执行的一组作业。每个作业在工作流程中独立运行。                                                                                                   |
| `check-bats-version:` | 工作流程中特定作业的标识符。此作业名为 `check-bats-version`。                                                                                                         |
| `runs-on:`            | 指定运行作业的机器类型。此处设置为在最新版本的 Ubuntu 上运行。                                                                                                        |
| `steps:`              | 包含将作为作业一部分执行的一系列任务（步骤）。                                                                                                                        |
| `uses:`               | 用于指定要作为步骤一部分包含的操作。例如，`actions/checkout@v4` 检出仓库，`actions/setup-node@v3` 设置 Node 环境。                                                        |
| `with:`               | 为操作指定附加参数。它与 `uses` 结合使用以配置操作。                                                                                                                  |
| `node-version:`       | `with` 下的参数，指定 `setup-node` 操作要设置的 Node.js 版本。在本例中，设置为版本 '14'。                                                                               |

### 事件

```yaml
name: Event-trigger-on-push-example # 事件触发-推送示例
on: [push] # 事件在此定义
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 运行一个脚本
        run: echo "此工作流程在每次推送到仓库时运行。"
```

**事件触发器**

| 事件名称                      | 说明                                          |
| :---------------------------- | :---------------------------------------------- |
| `push`                        | 在推送到仓库时触发。                              |
| `pull_request`                | 在拉取请求事件上触发。                            |
| `pull_request_review`         | 在拉取请求审查事件上触发。                        |
| `pull_request_review_comment` | 在拉取请求审查的评论上触发。                      |
| `pull_request_target`         | 用于分叉仓库中的工作流程。                        |
| `fork`                        | 在仓库被分叉时触发。                              |
| `issue_comment`               | 在问题和 PR 评论上触发。                         |
| `issues`                      | 在问题事件上触发。                                |
| `label`                       | 在标签事件上触发。                                |
| `milestone`                   | 在里程碑事件上触发。                              |
| `deployment`                  | 在部署时触发。                                  |
| `deployment_status`           | 在部署状态更新时触发。                            |
| `public`                      | 在仓库从私有变为公共时触发。                      |
| `repository_dispatch`         | 在自定义仓库事件上触发。                          |
| `schedule`                    | 按定义的计划触发。                                |
| `workflow_dispatch`           | 允许手动触发工作流程。                            |
| `workflow_run`                | 在另一个工作流程完成时触发。                      |
| `create`                      | 在创建分支或标签时触发。                          |
| `delete`                      | 在删除分支或标签时触发。                          |
| `page_build`                  | 在 GitHub Pages 构建事件上触发。                 |
| `release`                     | 在发布事件上触发。                                |
| `watch`                       | 在有人给仓库加星时触发。                          |
| `registry_package`            | 在注册表包事件上触发。                            |
| `status`                      | 在 Git 提交的状态更新时触发。                     |
| `project`                     | 在项目板事件上触发。                              |
| `project_card`                | 在项目卡片事件上触发。                            |
| `project_column`              | 在项目列事件上触发。                              |
| `member`                      | 在协作者事件上触发。                              |
| `gollum`                      | 在 Wiki 页面更新时触发。                         |

### 作业

单个作业：

```yaml
name: Single Job
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 运行构建脚本
        run: script/build
```

多个作业：

```yaml
name: CI Workflow
on: [push]
jobs:
  job-1:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 运行作业 1
        run: echo "正在运行作业 1"
  job-2:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 运行作业 2
        run: echo "正在运行作业 2"
  job-3:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 运行作业 3
        run: echo "正在运行作业 3"
```

### 步骤

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # 步骤 1
      - name: 检出仓库
        uses: actions/checkout@v2
      # 步骤 2
      - name: 设置 Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "14"
      # 步骤 3
      - name: 安装依赖项
        run: npm install
      # 步骤 4
      - name: 运行测试
        run: npm test
```

### GitHub 运行器和自托管运行器

[GitHub 托管的运行器](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners)：

```yaml
name: Workflow
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest # 默认运行器
    steps:
      - uses: actions/checkout@v2
      - name: 运行一个脚本
        run: echo "你好，世界！"
```

[自托管运行器](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners)

```yaml
name: Workflow with Self-Hosted Runner
on: [push]
jobs:
  build:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v2
      - name: 运行一个脚本
        run: echo "来自自托管运行器的问候！"
```

### 环境变量

使用环境定义的自定义变量。

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      CUSTOM_VARIABLE: "你好，世界！" # 使用 env 定义的自定义变量：
    steps:
      - name: 检查环境变量
        run: echo "CUSTOM_VARIABLE 的值是 $CUSTOM_VARIABLE"
```

### 秘密变量

要在您的 GitHub 仓库中添加新的秘密变量，请导航至 `仓库` > `设置` > `安全` >
`秘密变量和变量` > `Actions` > `新建仓库秘密变量`

秘密变量工作流程示例：

```yaml
name: Workflow with Secrets
on: [push]
jobs:
  example_job:
    runs-on: ubuntu-latest
    steps:
      - name: 检出仓库
        uses: actions/checkout@v2
      - name: 使用秘密变量
        run: echo "秘密变量是 ${{ secrets.MY_SECRET }}"
```

### 构建物

要访问您的构建物，请导航至 `仓库` > `Actions` > `工作流程运行` > `构建物`

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 构建项目
        run: make build
      - name: 上传构建物
        uses: actions/upload-artifact@v3 # 上传构建物的预构建操作
        with:
          name: my-artifact
          path: path/to/artifact
```

### 缓存依赖项

依赖项缓存存储工作流程中下载的包或已编译的二进制文件。

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: 缓存依赖项
        uses: actions/cache@v2 # 存储下载的包或已编译的二进制文件
        with:
          path: |
            path/to/dependencies
            another/path
          key: ${{ runner.os }}-deps-${{ hashFiles('**/lockfile') }} # 在操作系统中生成依赖项锁定文件的哈希值
      - name: 安装依赖项
        run: install-command
```

### 矩阵策略

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]
        # 矩阵策略运行使您能够在多种环境和操作系统的组合中运行作业
        os: [ubuntu-latest, windows-latest, macOS-latest]
    steps:
      - uses: actions/checkout@v2
      - name: 使用 Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm install
      - run: npm test
        env:
          CI: true
```

### 条件和表达式

分支条件：

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 检出代码
        uses: actions/checkout@v2
      - name: 运行构建
        if: github.ref == 'refs/heads/main' # "运行构建" 步骤仅在当前分支为 main 时执行。
        run: make build
```

事件触发条件：

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: 检出代码
        uses: actions/checkout@v2
      - name: 运行测试
        if: github.event_name == 'pull_request' # "运行测试" 步骤仅在工作流程由拉取请求事件触发时执行。
        run: npm test
```

### 工作流程命令

根据您的操作系统，如果您运行的是 ubuntu-latest，bash 命令应该可以工作。

```yaml
steps:
  - name: 设置环境变量
    run: echo "NAME=value" >> $GITHUB_ENV
```

### 并发

`concurrency` 字段根据 `github.head_ref` 创建一个组。如果在同一并发组内启动新的运行，它将取消任何正在进行的运行。

```yaml
jobs:
  my_job:
    runs-on: ubuntu-latest
    concurrency:
      group: ${{ github.head_ref }}
      cancel-in-progress: true
    steps:
      - name: 运行一个脚本
        run: echo "正在运行脚本..."
```

## 另请参阅

- [YAML](/yaml) _(r3f.cn)_
- [Github](/github) _(r3f.cn)_
- [GitHub Actions 文档](https://docs.github.com/en/actions)_(docs.github.com/en/actions)_
