---
title: Pandoc
date: 2023-03-21 13:26:00
background: bg-red-400
tags:
  - 转换
  - 文档
  - 实用工具
categories:
  - Linux 命令
intro: |
  [Pandoc](https://pandoc.org) 是一个文档转换器，这份 pandoc 速查表包含 pandoc 命令和一些常见的 pandoc 技巧。
plugins:
  - copyCode
---

## 入门指南

### Pandoc 用法

语法

```shell script
$ pandoc -s [源文件] -o [输出文件]
```

## Pandoc 示例

### LaTeX 转 MS Word {.col-span-2}

简单的 .tex 转 .docx

```shell script
$ pandoc -s file.tex -o file.docx
```

.tex 转 .docx（带默认引文）

```shell script
$ pandoc -s file.tex --citeproc --bibliography=bib_library.bib -o file.docx
```

.tex 转 .docx（带特定引文样式）

```shell script
$ pandoc -s file.tex --citeproc --bibliography=bib_library.bib --csl=apa.csl -o file.docx
```

从[这里](https://github.com/citation-style-language/styles)获取 `.csl` 文件

.tex 转 .docx（带交叉引用）

```shell script
$ pandoc -s file.tex --filter pandoc-crossref -o file.docx
```

从[这里](https://github.com/lierdakil/pandoc-crossref/releases)获取过滤器 `pandoc-crossref`

## 另请参阅 {.cols-1}

- [pandoc 示例](https://pandoc.org/demos.html)

