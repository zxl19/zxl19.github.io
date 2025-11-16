---
layout: post
title: C++防卫式声明
date: 2025-11-16
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++防卫式声明学习笔记。

<!-- more -->

## 防卫式声明

防卫式声明（include guards）是C++中用于防止同一头文件被重复包含的机制，目的是为了避免重复定义错误。

### 使用宏定义

1. 属于C++标准，所有编译器都支持；
2. 依赖唯一的宏名，宏名冲突会导致保护失效；
3. Google C++风格指南建议使用`<PROJECT>_<PATH>_<FILE>_H_`格式的宏名；
4. 重复包含时仍需要解析文件内容，编译速度较慢；

### 使用`#pragma once`

1. 不属于C++标准，是编译器扩展，几乎所有现代编译器都支持；
2. 依赖唯一的文件标识，通常是完整路径，相同内容的文件副本会导致保护失效；
3. 重复包含时会直接跳过，编译速度较快；

## 示例

两种防卫式声明方式可以同时使用，实现双重保护。以`foo`工程中的`foo/src/bar/baz.h`头文件为例进行说明：

```cpp
/**
 * @file baz.h
 * @author zxl19 (https://github.com/zxl19)
 * @brief 防卫式声明示例
 * @version 0.1
 * @date 2025-11-16
 *
 * @copyright Copyright (c) 2025
 *
 */
#pragma once

#ifndef FOO_BAR_BAZ_H_
#define FOO_BAR_BAZ_H_

// 头文件内容

#endif // FOO_BAR_BAZ_H_
```

## 参考

1. [include guards in C++-GeeksforGeeks](https://www.geeksforgeeks.org/cpp/include-guards-in-c/)
2. [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
3. [如何理解防卫式声明？-50包邮的回答-知乎](https://www.zhihu.com/question/59534480/answer/551143624)
4. [头文件的防卫式声明-编程实战的文章-知乎](https://zhuanlan.zhihu.com/p/336622992)
5. [C++防卫式声明-CSDN博客](https://blog.csdn.net/wo164683812/article/details/79312965)
