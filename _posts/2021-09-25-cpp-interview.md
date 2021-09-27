---
layout: post
title: C++面试知识点总结
date: 2021-09-25
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

C++面试知识点总结。

<!-- more -->

**整理中**

## C++ Hello World

### C++和C的区别

### 面向对象特征

1. **封装**；
2. **继承**；
3. **多态**；

## 关键字用法

### 关于`const`

### 关于`delete`

### 关于`enum`

### 关于`extern`

### 关于`friend`

### 关于`inline`

### 关于`static`

### 关于`this`

### 关于`typedef`

### 关于`virtual`

## 区别辨析

### 结构体`struct`和共用体`union`

### `#define`和`const`

### `size_t`和`int`

```cpp
typedef unsigned int size_t;    // 32位
typedef unsigned long size_t;   // 64位
```

与`int`固定四个字节不同，`size_t`的取值范围是目标平台下最大可能的数组尺寸，一些平台下`size_t`的范围小于`int`的正数范围，又或者大于`unsigned int`，使用`int`既有可能浪费，又有可能范围不够大。

### `NULL`和`nullptr`

为解决`NULL`代指空指针存在的二义性问题，在C++11中引入`nullptr`关键字来代指空指针。

```cpp
NULL        // 0
nullptr     // 空指针，C++11
```

## C++11

### 关于`auto`

### 关于`default`

### 关于`for`

### 关于智能指针

## 参考

1. [C++教程-菜鸟教程](https://www.runoob.com/cplusplus/cpp-tutorial.html)
2. [C++入门教程-C语言中文网](http://c.biancheng.net/cplus/)
3. [C++11教程-C语言中文网](http://c.biancheng.net/cplus/11/)
4. [校招C++大概学习到什么程度？-程序员内功修炼的回答-知乎](https://www.zhihu.com/question/290102232/answer/2094675219)
5. [siez_t和int1-CSDN博客](https://blog.csdn.net/wc11223/article/details/70553583)
6. [siez_t和int2-CSDN博客](https://blog.csdn.net/qq_41598072/article/details/84924997)
7. [NULL和nullptr-CSDN博客](https://blog.csdn.net/qq_18108083/article/details/84346655)
