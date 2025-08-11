---
layout: post
title: OpenMP库使用笔记
date: TODO
author: zxl19
tags: [C++, OpenMP, Note]
comments: true
toc: true
pinned: false
---

我的OpenMP库使用笔记。

<!-- more -->

## OpenMP Hello World

```shell
sudo apt install libomp-dev
```

## CMakeLists

```cmake
find_package(OpenMP REQUIRED QUIET)
if(OpenMP_FOUND)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")   # 这个编译选项实际上就是-fopenmp
endif()
```

## C++ API

详见`omp.h`。

## 示例

### ndt_omp

```cpp
#pragma omp parallel for num_threads(num_threads_) schedule(guided, 8)
```

### fast_gicp

```cpp
#pragma omp parallel for num_threads(num_threads_) firstprivate(k_indices, k_sq_dists) schedule(guided, 8)
#pragma omp parallel for num_threads(num_threads_) reduction(+ : sum_errors) schedule(guided, 8)
```

### small_gicp

```cpp
#pragma omp task
#pragma omp task default(shared) if (N > 512)
#pragma omp taskwait
#pragma omp single nowait
```

## 参考

1. [OpenMP](https://www.openmp.org)
2. [Options Controlling OpenMP and OpenACC-GCC](https://gcc.gnu.org/onlinedocs/gcc/OpenMP-and-OpenACC-Options.html)
3. [OpenMP-GCC](https://gcc.gnu.org/onlinedocs/gcc/OpenMP.html)
4. [GNU Offloading and Multi Processing Runtime Library-GCC](https://gcc.gnu.org/onlinedocs/libgomp/index.html)
5. [FindOpenMP-CMake Documentation](https://cmake.org/cmake/help/latest/module/FindOpenMP.html)
6. [OpenMP/sources](https://github.com/OpenMP/sources)
7. [koide3/ndt_omp](https://github.com/koide3/ndt_omp)
8. [koide3/fast_gicp](https://github.com/koide3/fast_gicp)
9. [koide3/small_gicp](https://github.com/koide3/small_gicp)
10. [OpenMP教程——从0开始一小时写出并行程序！-费米子的文章-知乎](https://zhuanlan.zhihu.com/p/397670985)
11. [OpenMP入门与实例分析-jdtang的文章-知乎](https://zhuanlan.zhihu.com/p/61857547)
12. [OpenMP（使用C++多线程并行计算优化你的程序）入门篇-只是无暇顾及的文章-知乎](https://zhuanlan.zhihu.com/p/608946001)
13. [OpenMP在实际开发中应用多吗？-笑到猝死的家伙的回答-知乎](https://www.zhihu.com/question/22347096/answer/1912952617950229190)
14. [OpenMP在实际开发中应用多吗？-Justin的回答-知乎](https://www.zhihu.com/question/22347096/answer/110724861536)
15. [openmp有必要存在吗,既然有了pthread?-昆冈玉的回答-知乎](https://www.zhihu.com/question/460601207/answer/2248436586)
16. [多线程加速矩阵运算:OpenMP vs. pthread-1234554321的文章-知乎](https://zhuanlan.zhihu.com/p/642882774)
17. [常用并行编程库都有哪些优缺点（threads.h，pthread，openmp等）？-bostonalen的回答-知乎](https://www.zhihu.com/question/642082042/answer/3413842844)
