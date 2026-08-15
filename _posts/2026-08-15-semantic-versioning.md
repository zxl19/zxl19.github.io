---
layout: post
title: 语义化版本学习笔记
date: 2026-08-15
author: zxl19
tags: [Git, Note]
comments: true
toc: true
pinned: false
---

我的语义化版本（Semantic Versioning，SemVer）学习笔记。

<!-- more -->

## 语义化版本

1. [Semantic Versioning 2.0.0](https://semver.org)
2. [Semantic Versioning](https://semantic-versioning.org)

## 合法语义化版本的BNF语法

```text
巴科斯-瑙尔范式（Backus–Naur Form，BNF）
```

```text
<valid semver> ::= <version core>
                 | <version core> "-" <pre-release>
                 | <version core> "+" <build>
                 | <version core> "-" <pre-release> "+" <build>

<version core> ::= <major> "." <minor> "." <patch>

<major> ::= <numeric identifier>

<minor> ::= <numeric identifier>

<patch> ::= <numeric identifier>

<pre-release> ::= <dot-separated pre-release identifiers>

<dot-separated pre-release identifiers> ::= <pre-release identifier>
                                          | <pre-release identifier> "." <dot-separated pre-release identifiers>

<build> ::= <dot-separated build identifiers>

<dot-separated build identifiers> ::= <build identifier>
                                    | <build identifier> "." <dot-separated build identifiers>

<pre-release identifier> ::= <alphanumeric identifier>
                           | <numeric identifier>

<build identifier> ::= <alphanumeric identifier>
                     | <digits>

<alphanumeric identifier> ::= <non-digit>
                            | <non-digit> <identifier characters>
                            | <identifier characters> <non-digit>
                            | <identifier characters> <non-digit> <identifier characters>

<numeric identifier> ::= "0"
                       | <positive digit>
                       | <positive digit> <digits>

<identifier characters> ::= <identifier character>
                          | <identifier character> <identifier characters>

<identifier character> ::= <digit>
                         | <non-digit>

<non-digit> ::= <letter>
              | "-"

<digits> ::= <digit>
           | <digit> <digits>

<digit> ::= "0"
          | <positive digit>

<positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
           | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
           | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
           | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
           | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
           | "y" | "z"
```

## 参考

1. [semver/semver](https://github.com/semver/semver)
2. [什么是语义化版本号SemVer(Semantic Versioning)？-路多辛的文章-知乎](https://zhuanlan.zhihu.com/p/620367392)
3. [Semantic Versioning规范-王文艺的文章-知乎](https://zhuanlan.zhihu.com/p/663530903)
