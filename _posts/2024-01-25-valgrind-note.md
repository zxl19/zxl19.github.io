---
layout: post
title: Valgrind使用笔记
date: 2024-01-25
author: zxl19
tags: [C++, Valgrind, Note]
comments: true
toc: true
pinned: false
---

我的Valgrind使用笔记。

<!-- more -->

## Valgrind Hello World

1. Valgrind是用于调试和分析Linux程序的工具；
2. Valgrind提供了工具套件，用于检测内存管理和线程错误问题：

    - Memcheck：用于检测内存管理问题，主要针对C和C++程序；
    - Cachegrind：缓存探查器（profiler），用于检测缓存问题；
    - Callgrind：Cachegrind的扩展，用于可视化调用图（callgraph）；
    - Massif：堆（heap）探查器，用于可视化堆使用情况；
    - Helgrind：线程（thread）调试器，用于检测多线程程序中的数据竞争（data race）；
    - DRD：用于检测多线程C和C++程序中的错误；
    - DHAT：用于检查程序的堆分配使用；
    - Experimental Tools：试验性工具；
    - Other Tools：其他工具；

3. 使用以下命令安装Valgrind：

    ```shell
    sudo apt install valgrind
    ```

## 命令说明

```shell
valgrind [valgrind-options] [your-program] [your-program-options]
```

## 常用语法

1. 使用默认的Memcheck工具检查程序的内存使用情况：

    ```shell
    valgrind program
    valgrind --tool=memcheck program
    ```

    常用于检查内存泄露，注意首次出现`Invalid read/write of size *`的位置，必要时可以关闭命令行中的调试输出。

2. 使用Memcheck工具详细报告程序所有可能的内存泄露：

    ```shell
    valgrind --tool=memcheck --leak-check=full --show-leak-kinds=all program
    ```

3. 使用Cachegrind工具评测并记录程序的CPU缓存操作：

    ```shell
    valgrind --tool=cachegrind program
    ```

4. 使用Massif工具评测并记录程序的堆内存和栈（stack）使用情况：

    ```shell
    valgrind --tool=massif --stacks=yes program
    ```

## 参考

1. [Valgrind](https://valgrind.org)
2. [linux valgrind 安装和使用-CSDN博客](https://blog.csdn.net/xianquji1676/article/details/106168317)
3. [valgrind基本功能介绍、基础使用方法说明-CSDN博客](https://blog.csdn.net/weixin_45518728/article/details/119865117)
4. [Linux性能分析valgrind（一）之memcheck使用-Xin Lee的文章-知乎](https://zhuanlan.zhihu.com/p/92074597)
5. [Linux性能分析valgrind（二）之callgrind使用-Xin Lee的文章-知乎](https://zhuanlan.zhihu.com/p/92082070)
6. [Linux性能分析valgrind（三）之DRD（死锁分析利器）-Xin Lee的文章-知乎](https://zhuanlan.zhihu.com/p/92098107)
7. [大型C++项目如何检测内存泄漏？-玩转Linux内核的回答-知乎](https://www.zhihu.com/question/382668081/answer/3154728722)
8. [Valgrind：Memcheck参数详解-CSDN博客](https://blog.csdn.net/weixin_45318758/article/details/96391449)
