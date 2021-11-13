---
layout: post
title: 使用clang-format格式化C++代码
date: 2021-11-04
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

近期注意到在不同C++项目中用`Tab`键缩进空格数不同，并且VS Code安装C/C++扩展在Ubuntu系统中格式化失败，经过排查使用clang-format格式化C++代码。

<!-- more -->

## 安装

```shell
sudo apt install clang-format
```

检查安装情况并查看使用方式：

```shell
clang-format -help
```

## 配置

### 格式配置

输出格式配置到配置文件：

```shell
clang-format -style=google -dump-config > .clang-format
```

### 扩展配置

在VS Code中的C/C++扩展中设置`可执行文件的完整路径`为`/usr/bin/clang-format`。

## 参考

1. [ClangFormat](https://clang.llvm.org/docs/ClangFormat.html)
2. [ClangFormatStyleOptions](https://clang.llvm.org/docs/ClangFormatStyleOptions.html)
3. [安装使用-博客园](https://www.cnblogs.com/liuyunbin/p/11538267.html)
4. [VS Code扩展配置-CSDN博客](https://blog.csdn.net/z456531/article/details/119849610)
5. [配置说明1-CSDN博客](https://blog.csdn.net/softimite_zifeng/article/details/78357898)
6. [配置说明2-CSDN博客](https://blog.csdn.net/z2066411585/article/details/82290477)
7. [VS Code+Clang-format格式化代码-一条放浪不羁的爬虫的文章-知乎](https://zhuanlan.zhihu.com/p/356143396)
