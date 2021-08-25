---
layout: post
title: ROS中输出调试信息
date: 2021-06-08
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

在ROS中输出调试信息的方法。

<!-- more -->

## 引入头文件

```cpp
#include <ros/console.h>
```

## 基础语法

```cpp
ROS_<verbosity level>[_STREAM][_<other>]
```

常用`ROS_<verbosity level>`宏定义进行不同详细程度的输出。

### 命令详解

表格中从上到下严重程度递增，默认详细程度为`ROS_INFO()`。。

| verbosity level | 含义 |
| :------ | :------|
| DEBUG | Information that you never need to see if the system is working properly. |
| INFO | Small amounts of information that may be useful to a user. |
| WARN | Information that the user may find alarming, and may affect the output of the application, but is part of the expected working of the system. |
| ERROR | Something serious (but recoverable) has gone wrong. |
| FATAL | Something unrecoverable has happened. |

调试信息在`rqt_console`中可以查看。

## 参考

1. [roscpp/Overview/Logging](http://wiki.ros.org/roscpp/Overview/Logging)
2. [Verbosity Levels](http://wiki.ros.org/Verbosity%20Levels)
