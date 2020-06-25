---
layout: post
title: 在Windows和Ubuntu系统下使用Github进行版本管理
date: 2020-06-25
author: zxl19
tags: [Github]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统下使用Github进行版本管理。

<!-- more -->

## Windows

使用Github Desktop进行管理，可以满足大部分需求。

## Ubuntu

使用VS Code，已经集成git命令，结合GitLens插件进行管理。

```shell
git config --global user.name "your name"
git config --global user.email "your@email.com"
```

```shell
ssh-keygen -t rsa -C "your@email.com"
```

```shell
ssh -T git@github.com
```

## 参考

1. [Github Desktop](https://desktop.github.com/)
2. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
