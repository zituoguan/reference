---
title: GnuPG
categories:
  - Linux 命令
intro:
  GnuPG 速查表，一款加密和签名软件。
---
## 入门指南

### 软件

Gpg4win 和 GPG Suite 具有特定于操作系统的功能。

* [GnuPG](https://gnupg.org/)
* [Gpg4win](https://www.gpg4win.org/) (Windows)
* [GPG Suite](https://gpgtools.org/) (macOS)

有时 GPG 密钥也被称为 PGP 密钥。它们是可互换的，因为它们都遵循 [OpenPGP 标准](https://www.rfc-editor.org/rfc/rfc9580.html)。

### 创建密钥对

生成您的密钥：

```shell script
$ gpg --generate-key
```

... 或完全配置您的密钥。

```shell script
$ gpg --generate-full-keys
```

**注意：** 选择一个强密码短语！加密的强度取决于您的密码短语的强度。

### 密钥管理

列出您的密钥：

```shell script
$ gpg --list-keys
```

列出您的私钥：

```shell script
$ gpg --list-secret-keys
```

导出您的公钥：

```shell script
$ gpg --export --armor <ID>
```

导出您的私钥：

```shell script
$ gpg --export-secret-key --armor <ID>
```

删除您的公钥：

```shell script
$ gpg --delete-key <ID>
```

删除您的私钥：

```shell script
$ gpg --delete-secret-key <ID>
```

## 加密

### 对称加密

使用密码短语加密：

```shell script
$ gpg -c <FILE>
```

使用 `-a` 标志加密为 ASCII 格式：

```shell script
$ gpg -ac <FILE>
```

使用 `-o` 标志设置输出文件路径：

```shell script
$ gpg -c <FILE> -o <PATH>
```

使用密码短语解密：

```shell script
$ gpg <FILE>
```

**注意：** 选择一个强密码短语！加密的强度取决于您的密码短语的强度。

### 非对称加密

使用公私钥加密：

```shell script
$ gpg -e -r <RECIPIENT> <FILE>
```

使用 `-a` 标志加密为 ASCII 输出：

```shell script
$ gpg -ea -r <RECIPIENT> <FILE>
```

使用 `-s` 标志加密并签名：

```shell script
$ gpg -se -r <RECIPIENT> <FILE>
```

添加多个接收者：

```shell script
$ gpg -e -r <RECIPIENT1> -r <RECIPIENT2> <FILE>
```

使用 `-o` 标志设置输出文件路径：

```shell script
$ gpg -e -o <PATH> -r <RECIPIENT> <FILE>
```

使用您的私钥解密：

```shell script
$ gpg <FILE>
```

将 `<RECIPIENT>` 替换为您目标接收者的[导入公钥](#importing-a-public-key) ID。

### 导入公钥

使用文件导入：

```shell script
$ gpg --import <FILE>
```

使用链接导入 (macOS/Linux)：

```shell script
$ curl <WEBSITE> | gpg --import
```

不要忘记签署导入的密钥：

```shell script
$ gpg --sign-key <ID>
```

## 提交签名

### 本地 Git 设置

启用 GPG 签名：

```shell script
$ git config --global commit.gpgsign true
```

设置签名密钥：

```shell script
$ git config --global user.signingkey <ID>
```

设置 GPG 位置：

```shell script
$ git config --global gpg.program <PROGRAM>
```

**注意：** 您在 Git 和 GnuPG 中的姓名和电子邮件必须匹配。

### GPG 程序列表

将 `<PROGRAM>` 替换为以下之一：

| 平台        | 值                                         |
| ----------- | ------------------------------------------ |
| Windows     | `C:\Program Files (x86)\GnuPG\bin\gpg.exe` |
| macOS/Linux | /usr/local/bin/gpg                         |

{.left-text}

### 导出您的公钥

导出为 ASCII 格式：

```shell script
$ gpg --export --armor <ID>
```

**注意：** 像 GitHub 这样的平台可能会要求您验证在 Git 和 GnuPG 中设置的电子邮件。

## Windows：添加到启动应用 {.cols-1}

### PowerShell 命令

当您完全重启时，GPG 代理可能不会自动启动。使用 PowerShell 将 GnuPG 的 IPC 工具添加到启动应用中：

```shell script
$ $shell = New-Object -ComObject WScript.Shell
$ $shortcut = $shell.CreateShortcut("C:\Users\$($Env:UserName)\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\gpg-connect-agent.lnk")
$ $shortcut.TargetPath = "C:\Program Files (x86)\GnuPG\bin\gpg-connect-agent.exe"
$ $shortcut.Arguments = "/bye"
$ $shortcut.Save()
```

或者手动启动：

```shell script
$ gpgconf --launch gpg-agent
```

在[此处](ms-settings:startupapps)检查是否已成功添加。
