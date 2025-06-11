---
title: OpenSSL
date: 2020-11-25 18:28:43
icon: icon-style
background: bg-emerald-600
tags:
categories:
  - Linux 命令
intro: |
  这是与电子证书交互时使用的命令参考。
plugins:
  - copyCode
---

## 私钥 {.cols-2}

### 打印私钥详情

```bash
openssl rsa -check -text -in privateKey.key
```

### 打印私钥的哈希值

```bash
openssl rsa -noout -modulus -in privateKey.key | openssl md5
openssl rsa -noout -modulus -in privateKey.key | openssl sha1
openssl rsa -noout -modulus -in privateKey.key | openssl sha256
openssl rsa -noout -modulus -in privateKey.key | openssl sha512
```

### 修改密码

```bash
openssl rsa -aes256 -in privateKey.key -out newPrivateKey.key
```

### 列出可用的椭圆曲线

```bash
openssl ecparam -list_curves
```

### 使用特定曲线创建椭圆曲线私钥

```bash
openssl ecparam -name secp521r1 -genkey -noout -out privateKey.key
```

## 证书 {.cols-2}

### 打印证书的哈希值

```bash
openssl x509 -noout -modulus -in certificate.crt | openssl md5
openssl x509 -noout -modulus -in certificate.crt | openssl sha1
openssl x509 -noout -modulus -in certificate.crt | openssl sha256
openssl x509 -noout -modulus -in certificate.crt | openssl sha512
```

或者，也可以这样：

```bash
openssl x509 -noout -fingerprint -in certificate.crt
openssl x509 -noout -fingerprint -sha256 -in certificate.crt
```

### 打印证书内容

```bash
openssl x509 -in certificate.crt -noout -text|more
```

### 打印证书的特定字段

```bash
openssl x509 -noout -subject certificate.crt
openssl x509 -noout -issuer certificate.crt
openssl x509 -noout -dates certificate.crt
```

### 检查服务器证书

```bash
echo | openssl s_client -servername www.openssl.org -connect \
www.openssl.org:443 2>/dev/null | openssl x509 -noout -text|more
echo | openssl s_client -servername imap.arcor.de -connect \
imap.arcor.de:993 2>/dev/null | openssl x509 -noout -text|more
```

### 验证证书

**正常**

```bash
openssl verify -verbose -x509_strict -CAfile \
issuer.crt Test\ Haeschen\ 1.crt
```

结果:

```bash
Test Haeschen 1.crt: OK
```

**损坏**
（[例如](https://security.stackexchange.com/questions/60804/creating-an-x-509-certificate-with-an-invalid-signature)）

```bash
openssl verify -verbose -x509_strict -CAfile \
issuer.crt Test\ Haeschen\ 1_corrupted.crt
```

结果:

```bash
C = DE, ST = Thueringen, L = Rudolstadt, O = Damaschkestr. 11, OU = Arbeitszimmer, CN = Test Haeschen 1
error 7 at 0 depth lookup: certificate signature failure
error Test Haeschen 1_corrupted.crt: verification failed
40270500477F0000:error:0200008A:rsa routines:RSA_padding_check_PKCS1_type_1:invalid padding:../crypto/rsa/rsa_pk1.c:75:
40270500477F0000:error:02000072:rsa routines:rsa_ossl_public_decrypt:padding check failed:../crypto/rsa/rsa_ossl.c:598:
40270500477F0000:error:1C880004:Provider routines:rsa_verify:RSA lib:../providers/implementations/signature/rsa_sig.c:774:
40270500477F0000:error:06880006:asn1 encoding routines:ASN1_item_verify_ctx:EVP lib:../crypto/asn1/a_verify.c:217:
```

## S/Mime {.cols-2}

### 创建签名

```bash
openssl smime -sign -in msg.txt -text -out msg.p7s \
-signer certificate.crt -inkey privateKey.key
```

### 验证签名

```bash
openssl smime -verify -in msg.p7s -CAfile chain.pem
```

## CRL {.cols-2}

### 打印 CRL 内容

```bash
openssl crl -inform DER -noout -text  -in crl/cacrl.der
openssl crl -inform PEM -noout -text  -in crl/cacrl.pem
```

## PKCS#12 {.cols-2}

### 显示内容

```bash
openssl pkcs12 -info -in  digitalIdentity.p12
```

### 从证书和私钥创建

```bash
openssl pkcs12 -export -in certificate.cert \
-inkey privateKey.key -out digitalIdentity.p12
```

### 提取私钥

```bash
openssl pkcs12 -in digitalIdentity.p12 -out privateKey.key
```

### 转换为 PEM

```bash
openssl pkcs12 -in digitalIdentity.p12 -out digitalIdentity.pem
```

## TSA {.cols-2}

### 显示查询

```bash
openssl ts -query -in query.tsq -text
```

### 显示回复

```bash
openssl ts -reply -in reply.tsr -text
```

### 验证回复

```bash
openssl ts -verify -in reply.tsr -data data.dat -CAfile chain.pem
```

### 从回复中提取令牌

```bash
openssl ts -reply -in reply.tsr -token_out -out token.tk
```

### 从令牌中提取证书

```bash
openssl pkcs7 -inform DER -in token.tk -print_certs -noout -text
```

## CSR {.cols-2}

### 从现有密钥创建

```bash
openssl req -new -key privateKey.key -out my.csr
```

这当然可以是 RSA 密钥或基于椭圆曲线的密钥。可用的曲线可以使用以下命令列出：

```bash
openssl ecparam -list_curves
```

然后选择一条曲线并像这样创建一个私钥：

```bash
openssl ecparam -name secp521r1 -genkey -noout \
-out privateKey.key
```

### 显示

```bash
openssl req -in my.csr -noout -text
```

## HTTPS {.cols-2}

### 转储 PEM 编码的证书

```bash
openssl s_client -showcerts -connect www.example.com:443
```

## STARTTLS {.cols-2}

### 转储 PEM 编码的证书

```bash
openssl s_client -showcerts -starttls imap \
-connect mail.domain.com:139
```

## S/MIME 验证 {.cols-2}

### 可能的结果

消息被篡改（返回码 4）：

```bash
Verification failure
140485684135232:error:2E09A09E:CMS routines:CMS_SignerInfo_verify_content:verification failure:../crypto/cms/cms_sd.c:847:
140485684135232:error:2E09D06D:CMS routines:CMS_verify:content verify error:../crypto/cms/cms_smime.c:393:
```

消息签名不受信任（返回码 4）：

```bash
Verification failure
140146111432000:error:2E099064:CMS routines:cms_signerinfo_verify_cert:certificate verify error:../crypto/cms/cms_smime.c:252:Verify error:unable to get local issuer certificate
```

消息未签名（返回码 2）：

```bash
Error reading S/MIME message
140701208487232:error:0D0D40CD:asn1 encoding routines:SMIME_read_ASN1:invalid mime type:../crypto/asn1/asn_mime.c:469:type: multipart/alternative
```

验证成功（返回码 0）：

```bash
Verification successful
```

### 验证电子邮件消息的有效性

```bash
openssl cms -verify -in some_email_message.eml
```

### 明确指定信任来验证电子邮件消息的有效性

```bash
openssl cms -verify -in some_email_message \
-CAfile trust_anchor-crt
```

### 签名和加密的消息需要先解密：

注意：保存数字身份的 P12 文件必须是 pem 编码的！（见上文）

```bash
openssl cms -decrypt -out decrypted_email_message \
-inkey p12.pem -in some_encrypted_email_message
```

## 原始数据 {.cols-2}

### 查看 ASN.1 文件的原始结构（仅适用于 DER 编码的文件）

```bash
openssl asn1parse -in mysterious_file.pem
```

### 更详细一些

```bash
openssl asn1parse -dump -strictpem -in mysterious_file.pem
```

## 一些有用的 OpenSSL 命令资源

- [OpenSSL 命令备忘单](https://www.freecodecamp.org/news/openssl-command-cheatsheet-b441be1e8c4a/)
- [21 个 OpenSSL 示例助您应对实际场景](https://geekflare.com/openssl-commands-certificates/)
- [最常用的 OpenSSL 命令](https://www.sslshopper.com/article-most-common-openssl-commands.html)
- [OpenSSL 快速参考指南](https://www.digicert.com/ssl-support/openssl-quick-reference-guide.htm)
- [openssl_commands.md](https://gist.github.com/webtobesocial/5313b0d7abc25e06c2d78f8b767d4bc3)
- [OpenSSL 基础：使用 SSL 证书、私钥和 CSR](https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs)
- [OpenSSL 技巧和窍门](https://commandlinefanatic.com/cgi-bin/showarticle.cgi?article=art030)
- [使用 OpenSSL 检查远程证书链](https://langui.sh/2009/03/14/checking-a-remote-certificate-chain-with-openssl/)
- [OpenSSL：如何从 RFC3161 时间戳回复中提取证书和令牌状态？](https://stackoverflow.com/questions/66044640/openssl-how-to-extract-certificates-and-token-status-from-rfc3161-timestamping)
- [使用 openssl 为 SAN 证书生成 CSR 的步骤](https://www.golinuxcloud.com/openssl-subject-alternative-name/)
- [如何在证书签名请求中添加主题备用名称扩展](https://support.microfocus.com/kb/doc.php?id=3522065)

