---
layout: post
title: glog库学习笔记
date: TODO
author: zxl19
tags: [C++, glog, Note]
comments: true
toc: true
pinned: false
---

我的glog库学习笔记。

<!-- more -->

## CMakeLists

```cmake
cmake_minimum_required(VERSION 3.16)
project(myproj VERSION 1.0)

find_package(glog 0.6.0 REQUIRED)

add_executable(myapp main.cpp)
target_link_libraries(myapp glog)
```

## 示例

```cpp
#include <glog/logging.h>

int main(int argc, char* argv[]) {
    // Initialize Google’s logging library.
    google::InitGoogleLogging(argv[0]);

    // ...
    LOG(INFO) << "Found " << num_cookies << " cookies";
}
```

## 参考

1. [google/glog](https://github.com/google/glog)
