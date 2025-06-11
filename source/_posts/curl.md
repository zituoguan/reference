---
title: Curl
date: 2023-01-03 15:18:34
background: bg-slate-600
tags:
  - url
  - request
categories:
  - Linux 命令
intro: |
  这份 [Curl](https://github.com/curl/curl) 速查表包含了一些常用 Curl技巧的命令和示例。
plugins:
  - copyCode
---

## 入门指南

### 简介

`Curl` 是一款用于在服务器之间传输数据的工具，支持多种协议，包括：

- HTTP
- HTTPS
- FTP
- IMAP
- LDAP
- POP3
- SCP
- SFTP
- SMB
- SMTP
- 等等...

{.cols-3 .marker-none}

---

- [Curl GitHub 源代码仓库](https://github.com/curl/curl) _(github.com)_
- [Curl 官方网站](https://curl.se/) _(curl.se)_

### 选项 {.col-span-2 row-span-2}

```bash
-o <文件>    # --output: 写入文件
-u 用户名:密码 # --user: 认证
```

---

```bash
-v   # --verbose: 操作期间使 curl 输出详细信息
-vv  # 更详细
-s   # --silent: 不显示进度条或错误
-S   # --show-error: 与 --silent (-sS) 一起使用时，显示错误但不显示进度条
```

---

```bash
-i  # --include: 在输出中包含 HTTP 头部
-I  # --head: 仅头部信息
```

### 请求

```bash
-X POST # --request
-L # 如果页面重定向，则跟随链接
-F # --form: 用于 multipart/form-data 的 HTTP POST 数据
```

### 数据

```bash
# --data: HTTP POST 数据
# URL 编码 (例如, status="Hello")
-d '数据'

# --data 传递文件
-d @文件

# --get: 通过 get 发送 -d 数据
-G
```

### 头部信息

```bash
-A <字符串>      # --user-agent

-b 名称=值   # --cookie

-b, --cookie 文件           # 从指定文件加载 URL 的 cookie
-c, --cookie-jar 文件       # 将 URL 的 cookie 保存到指定文件

-H "X-Foo: y" # --header

--compressed  # 使用 deflate/gzip
```

### SSL

```bash
    --cacert <文件>
    --capath <目录>
```

```bash
-E, --cert <证书> # --cert: 客户端证书文件
    --cert-type # der/pem/eng
-k, --insecure # 用于自签名证书
```

#### 安装

```bash
apk add --update curl # 在 alpine linux 中安装
```

## 示例 {.cols-6}

### CURL GET/HEAD {.col-span-4 .row-span-2}

| 命令                                                                  | 描述                         |
| :-------------------------------------------------------------------- | :---------------------------------- |
| `curl -I https://r3f.cn`                                     | `curl` 发送请求              |
| `curl -v -I https://r3f.cn`                                  | `curl` 带详细信息的请求         |
| `curl -X GET https://r3f.cn`                                 | 为 `curl` 使用显式 http 方法 |
| `curl --noproxy 127.0.0.1 http://www.stackoverflow.com`               | 不使用 http 代理的 `curl`           |
| `curl --connect-timeout 10 -I -k https://r3f.cn`             | `curl` 默认没有超时    |
| `curl --verbose --header "Host: www.mytest.com:8182" r3f.cn` | `curl` 获取额外头部             |
| `curl -k -v https://www.google.com`                                   | `curl` 获取带头部的响应    |

### 多文件上传 {.col-span-2}

```bash
$ curl -v --include \
--form key1=value1 \
    --form upload=@本地文件名 URL
```

### 美化 curl 响应的 json 输出 {.col-span-2}

```bash
$ curl -XGET http://${elasticsearch_ip}:9200/_cluster/nodes | python -m json.tool
```

### CURL POST {.col-span-4}

| 命令                                                                     | 描述         |
| :-------------------------------------------------------------------------- | :------------------ |
| `curl -d "name=username&password=123456" <URL>`                             | `curl` 发送请求 |
| `curl <URL> -H "content-type: application/json" -d "{ \"woof\": \"bark\"}"` | `curl` 发送 json   |

### CURL 脚本安装 rvm {.col-span-2}

```shell
curl -sSL https://get.rvm.io | bash
```

### CURL 高级用法 {.col-span-6}

| 命令                                                                                     | 描述                    |
| :------------------------------------------------------------------------------------------ | :----------------------------- |
| `curl -L -s http://ipecho.net/plain, curl -L -s http://whatismijnip.nl`                     | 获取我的公网 `IP`             |
| `curl -u $username:$password http://repo.dennyzhang.com/README.txt`                         | 带凭据的 `curl`        |
| `curl -v -F key1=value1 -F upload=@本地文件名 <URL>`                                     | `curl` 上传                  |
| `curl -k -v --http2 https://www.google.com/`                                                | 使用 http2 的 curl                 |
| `curl -T cryptopp552.zip -u test:test ftp://10.32.99.187/`                                  | curl `ftp` 上传              |
| `curl -u test:test ftp://10.32.99.187/cryptopp552.zip -o cryptopp552.zip`                   | curl `ftp` 下载            |
| `curl -v -u admin:admin123 --upload-file package1.zip http://mysever:8081/dir/package1.zip` | 带凭据上传的 `curl` |

### 检查网站响应时间 {.col-span-4}

```shell
curl -s -w \
'\n查询时间:\t%{time_namelookup}\n连接时间:\t%{time_connect}\n应用连接时间:\t%{time_appconnect}\n重定向时间:\t%{time_redirect}\n预传输时间:\t%{time_pretransfer }\n开始传输时间:\t%{time_starttransfer}\n\n总时间:\t%{time_total}\n' \
     -o /dev/null https://www.google.com
```

### 使用 Curl 检查远程资源是否可用 {.col-span-2}

```bash
curl -o /dev/null --silent -Iw "%{http_code}" https://example.com/my.remote.tarball.gz
```

### 下载文件 {.col-span-3}

```bash
curl https://example.com | \
grep --only-matching 'src="[^"]*.[png]"' | \
cut -d \" -f2 | \
while read i; do curl https://example.com/"${i}" \
-o "${i##*/}"; done
```

从网站下载所有 PNG 文件 (使用 GNU grep)

### 下载文件，保存文件时不更改其名称 {.col-span-3}

```bash
curl --remote-name "https://example.com/linux-distro.iso"
```

重命名文件

```bash
curl --remote-name "http://example.com/index.html" --output foo.html
```

### 继续部分下载 {.col-span-3}

```bash
curl --remote-name --continue-at -"https://example.com/linux-distro.iso"
```

### 从多个域下载文件 {.col-span-3}

```bash
curl "https://www.{example,w3,iana}.org/index.html" --output "file_#1.html"
```

### 下载一系列文件 {.col-span-3}

```bash
curl "https://{foo,bar}.com/file_[1-4].webp" --output "#1_#2.webp"
```

下载一系列文件 (输出 `foo_file1.webp`, `foo_file2.webp...bar_file1_webp` 等)

### 重定向输出到文件 {.col-span-3}

```bash
$ curl http://url/file > file
```

### 基本认证 {.col-span-3}

```bash
$ curl --user 用户名:密码 http://example.com/
$ curl -u 用户名:密码 http://example.com/
```

### 写入文件而不是标准输出 {.col-span-2}

```bash
$ curl -o 文件 http://url/文件
$ curl --output 文件 http://url/文件
```

### 下载头部信息

```bash
$ curl -I url
# 显示头部信息
```

### 将输出写入名为 remote_file 的文件 {.col-span-2}

```bash
$ curl -o 文件 http://url/文件
$ curl --output 文件 http://url/文件
```

### 执行远程脚本 {.col-span-2}

```bash
$ curl -s http://url/myscript.sh
```

### 配置文件 {.col-span-2}

```bash
curl -K 文件
# 从文件读取配置
curl --config 文件
$HOME/.curlrc # UNIX 类系统上的默认配置文件
```
