---
layout: post
title: 在Windows和Ubuntu系统下使用GitHub进行版本管理
date: 2020-06-25
author: zxl19
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统下使用GitHub进行版本管理。

<!-- more -->

## Windows

使用GitHub Desktop进行管理，可以满足大部分需求。

## Ubuntu

使用VS Code，已经集成git命令，结合GitLens插件进行管理。

1. 设置全局变量

    ```shell
    git config --global user.name "your name"
    git config --global user.email "your@email.com"
    ```

2. 创建SSH key

    ```shell
    ssh-keygen -t rsa -C "your@email.com"
    ```

    连续点三次回车确认。

3. 保存SSH key

    复制`~/.ssh/id_rsa.pub`中的内容，在GitHub中`Setting`->`SSH and GPG keys`中添加新的SSH key。

4. 完成通信设置

    ```shell
    ssh -T git@github.com
    ```

    输入`yes`确认。

5. 首次使用需要在GitHub网站上进行验证，授权VS Code登录

## 参考

1. [GitHub Desktop](https://desktop.github.com/)
2. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
