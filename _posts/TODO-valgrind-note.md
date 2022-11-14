---
layout: post
title: valgrind学习笔记
date: TODO
author: zxl19
tags: [C++, valgrind, Note]
comments: true
toc: true
pinned: false
---

我的GDB学习笔记。

<!-- more -->

##

```shell
sudo apt install valgrind
```

```shell
valgrind [valgrind-options] [your-program] [your-program-options]
```

```shell
valgrind --tool=memcheck <program>
```

## 参考

1. [Linux性能分析valgrind（一）之memcheck使用-Xin Lee的文章-知乎](https://zhuanlan.zhihu.com/p/92074597)
2. [linux valgrind 安装和使用-CSDN博客](https://blog.csdn.net/xianquji1676/article/details/106168317)
