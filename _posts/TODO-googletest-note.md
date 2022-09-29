---
layout: post
title: GoogleTest库学习笔记
date: TODO
author: zxl19
tags: [C++, GoogleTest, Note]
comments: true
toc: true
pinned: false
---

我的GoogleTest库学习笔记。

<!-- more -->

## CMakeLists

```cmake
cmake_minimum_required(VERSION 3.14)
project(my_project)

# GoogleTest requires at least C++14
set(CMAKE_CXX_STANDARD 14)

add_executable(
  hello_test
  hello_test.cc
)
target_link_libraries(
  hello_test
  gtest
)
```

## 示例

```cpp
#include <gtest/gtest.h>

// Demonstrate some basic assertions.
TEST(HelloTest, BasicAssertions) {
  // Expect two strings not to be equal.
  EXPECT_STRNE("hello", "world");
  // Expect equality.
  EXPECT_EQ(7 * 6, 42);
}
```

## 参考

1. [google/googletest](https://github.com/google/googletest)
2. [GoogleTest User’s Guide](https://google.github.io/googletest/)
