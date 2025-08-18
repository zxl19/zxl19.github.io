---
layout: post
title: 在Ubuntu系统中执行脚本
date: 2025-08-12
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中执行脚本。

<!-- more -->

## 使用`source`命令

### 命令说明

1. 在**当前shell**中执行脚本中的命令；
2. 常用于设置环境变量；

### 常用语法

1. 执行指定脚本：

    ```shell
    source path/to/file
    ```

2. 执行指定脚本（使用`.`代替`source`）：

    ```shell
    . path/to/file
    ```

## 使用命令行解释器

包括`sh`、`bash`、`zsh`等，启动一个子shell，在**子shell**中执行脚本中的命令，不会影响当前shell环境。

## 参考

1. [为什么Shell命令用sh和用source执行会不一样？-Dailylucky的回答-知乎](https://www.zhihu.com/question/27673228/answer/2894777395)
2. [【Linux】详解shell中source、sh、bash、./执行脚本的区别-CSDN博客](https://blog.csdn.net/houxiaoni01/article/details/105161356)
3. [Linux执行脚本时source和.和sh和./的区别-博客园](https://www.cnblogs.com/FengZeng666/p/15323028.html)
4. [linux里source、sh、bash、./有什么区别-博客园](https://www.cnblogs.com/pcat/p/5467188.html)
