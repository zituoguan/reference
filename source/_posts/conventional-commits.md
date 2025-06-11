---
title: Conventional Commits (约定式提交)
date: 2024-03-11 09:51:44
background: bg-[#e86d7a]
tags:
  - permission
categories:
  - 其他
intro: |
  一份 Conventional Commits (约定式提交) 和 Conventional Comments (约定式注释) 标准的速查表
plugins:
---

## 入门指南 {.cols-3}

### 快速指南

#### 为什么使用约定式提交

- 易于遵循的提交信息结构。
- 清晰地说明变更的性质。
- 确保团队间提交信息的一致性。
- 支持自动化版本控制和变更日志生成。
- 使提交历史易于浏览。
- 允许指定“范围”以获得更清晰的说明。
- 对破坏性变更有特殊标记。
- 促进团队成员之间更好的理解。
- 使审查过程更高效。
- 通过描述性的提交信息帮助未来进行故障排除。

#### 结构

```javascript
<类型>[可选 范围]: <描述>

[可选 正文]

[可选 脚注]
```

[官方网站](https://www.conventionalcommits.org/zh-hans/) {.link-arrow}

### 示例

- feat: 添加 jwt 支持
- feat!: API 中的破坏性变更
- feat!(ui): 重新设计用户个人资料页面
- fix: 修复 SQL 注入漏洞
- fix(database): 解决数据竞争条件
- docs: 更新 README 的设置部分
- style(login): 修正登录组件中的缩进
- refactor: 重构用户数据库模式
- perf: 优化用户检索代码以加快响应速度
- test: 为 jwt 身份验证添加测试
- test(payment): 为支付网关添加测试
- chore: 更新构建脚本
- chore(deps): 更新依赖项
- build(docker): 更新 Dockerfile 以使用 node 14
- ci: 为集成测试添加作业
- revert: 还原提交 a1b2c3d4e5f

### 类型

| 类型     | 描述                                                                                                     |
| -------- | ---------------------------------------------------------------------------------------------------------------- |
| `feat`   | 引入新功能                                                                                                       |
| `fix`    | 修复缺陷                                                                                                       |
| `docs`   | 仅文档变更                                                                                                     |
| `style`  | 不影响功能的代码变更（例如，格式化、空白等）                                                                       |
| refactor | 既不修复缺陷也不引入新功能的代码变更，通常用于改进代码可读性或结构                                                       |
| perf     | 提升性能的代码变更                                                                                                 |
| test     | 添加缺失的测试或修正现有测试                                                                                       |
| `chore`  | 不修改源代码或测试文件的变更，例如调整构建过程或添加依赖项                                                               |
| build    | 影响构建系统或外部依赖项的变更（例如，webpack、npm 包的变更）                                                        |
| ci       | 对持续集成配置文件和脚本的变更（例如，Travis、CircleCI、Jenkins）                                                    |
| revert   | 还原先前进行的提交                                                                                                 |

{.bold-first}

## 规范 {.cols-1}

### 规范

- 提交必须以类型为前缀，该类型由名词（feat、fix 等）组成，后跟可选的作用域、可选的 !，以及必需的冒号和空格。
- 当提交为您的应用程序或库添加新功能时，必须使用类型 feat。
- 当提交代表对您的应用程序的错误修复时，必须使用类型 fix。
- 可以在类型之后提供作用域。作用域必须由描述代码库某个部分的名词组成，并用圆括号括起来，例如 `fix(parser):`
- 描述必须紧跟在类型/作用域前缀后的冒号和空格之后。描述是对代码更改的简短总结，例如：`fix: array parsing issue when multiple spaces were contained in string.`
- 可以在简短描述之后提供更长的提交正文，提供有关代码更改的附加上下文信息。正文必须在描述后空一行开始。
- 提交正文是自由格式的，可以包含任意数量的换行分隔段落。
- 可以在正文后空一行提供一个或多个脚注。每个脚注必须包含一个单词标记，后跟 `: ` 或 ` #` 分隔符，然后是一个字符串值（这受到 [git trailer 约定](https://git-scm.com/docs/git-interpret-trailers) 的启发）。
- 脚注的标记必须使用 `-` 代替空格字符，例如 `Acked-by`（这有助于区分脚注部分和多段落正文）。BREAKING CHANGE 是一个例外，它也可以用作标记。
- 脚注的值可以包含空格和换行符，当观察到下一个有效的脚注标记/分隔符对时，解析必须终止。
- 破坏性变更必须在提交的类型/作用域前缀中指出，或作为脚注中的条目。
- 如果作为脚注包含，破坏性变更必须由大写文本 BREAKING CHANGE 组成，后跟冒号、空格和描述，例如：`BREAKING CHANGE: environment variables now take precedence over config files.`
- 如果包含在类型/作用域前缀中，则必须通过紧接在 `:` 之前的 `!` 来指示破坏性变更。如果使用 `!`，则可以从脚注部分省略 `BREAKING CHANGE:`，并且提交描述应用于描述破坏性变更。
- 除了 feat 和 fix 之外的类型也可以在您的提交消息中使用，例如：`docs: update ref docs.`
- 构成约定式提交的信息单元，除了必须大写的 BREAKING CHANGE 外，实现者不应将其视为区分大小写。
- 当在脚注中用作标记时，BREAKING-CHANGE 必须与 BREAKING CHANGE 同义。

## 另请参阅

- [Conventional Commits (约定式提交)](https://conventionalcommits.org/zh-hans/) _(conventionalcommits.org)_
