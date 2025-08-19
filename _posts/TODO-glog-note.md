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

## glog Hello World

1. glog（Google Logging）是谷歌开发的应用级日志库，支持C++14标准；
2. glog提供了基于C++风格的流形式API和辅助宏；
3. 使用时需要包含头文件：

    ```cpp
    #include <glog/logging.h>
    ```

**2025年8月：glog已于2025年6月30日停止维护。**

## CMakeLists

```cmake
cmake_minimum_required(VERSION 3.16)
project(myproj VERSION 1.0)

find_package(glog 0.7.1 REQUIRED)

add_executable(myapp main.cpp)
target_link_libraries(myapp glog::glog)
```

## 日志输出

### 日志等级

1. 根据严重程度从低到高：

    - `INFO`：正常信息；
    - `WARNING`：警告；
    - `ERROR`：错误；
    - `FATAL`：致命错误，强制结束程序；

2. 高等级日志也会输出到低等级日志对应的日志文件中，例如`ERROR`级别的日志也会输出到`WARNING`和`INFO`级别日志对应的日志文件中；

### 日志文件

1. 默认日志文件路径：

```text
<tmp>/<program name>.<hostname>.<user name>.log.<severity level>.<date>-<time>.<pid>
```

## 日志格式

```text
Lyyyymmdd hh:mm:ss.uuuuuu threadid file:line] msg...
```

## 示例

```cpp
#include <glog/logging.h>

int main(int argc, char* argv[]) {
    google::InitGoogleLogging(argv[0]);
    LOG(INFO) << "Found " << num_cookies << " cookies";
}
```

## 参考

1. [google/glog](https://github.com/google/glog)
2. [Google Logging Library](https://google.github.io/glog/stable/)
