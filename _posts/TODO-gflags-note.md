---
layout: post
title: gflags库学习笔记
date: TODO
author: zxl19
tags: [C++, gflags, Note]
comments: true
toc: true
pinned: false
---

我的gflags库学习笔记。

<!-- more -->

## CMakeLists

```cmake
# 本地安装
find_package(gflags REQUIRED QUIET)
# 三方库
add_subdirectory(gflags)

add_executable(foo main.cc)
target_link_libraries(foo gflags)
```

## 参考

1. [gflags/gflags](https://github.com/gflags/gflags)
2. [How To Use gflags](https://gflags.github.io/gflags/)
