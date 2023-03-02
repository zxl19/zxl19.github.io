---
layout: post
title: ROS中设置日志输出
date: 2021-06-08
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

在ROS中设置日志输出的方法。

<!-- more -->

## ROS日志输出

1. 需要包含头文件：

    ```cpp
    #include <ros/console.h>
    ```

2. ROS定义了`ROS_*`形式的宏，用于表示不同类型的日志输出：

    ```cpp
    ROS_<verbosity level>[_STREAM][_<other>]
    ```

3. 日志输出可以在终端中或者`rqt_console`中查看；

## 日志详细级别

| verbosity level | 含义 |
| :------ | :------|
| `DEBUG` | Information that you never need to see if the system is working properly. |
| `INFO` | Small amounts of information that may be useful to a user. |
| `WARN` | Information that the user may find alarming, and may affect the output of the application, but is part of the expected working of the system. |
| `ERROR` | Something serious (but recoverable) has gone wrong. |
| `FATAL` | Something unrecoverable has happened. |

1. 表格中从上到下的详细级别（verbosity level）依次提高，其严重程度也依次提高；
2. ROS默认输出`INFO`及以上详细级别的日志；
3. 可以通过以下五种方式设置日志输出的最低详细级别：

    - 修改`${ROS_ROOT}/config/rosconsole.config`文件：

        ```text
        log4j.logger.ros=INFO
        log4j.logger.ros.roscpp.superdebug=WARN
        ```

    - 使用`rqt_logger_level`的图形化交互界面设置：

        ```shell
        rosrun rqt_logger_level rqt_logger_level
        ```

    - 使用`rqt_console`的图形化交互界面设置：

        ```shell
        rqt_console
        ```

    - 使用`rosconsole`命令行工具设置：

        ```shell
        rosconsole get <node> <logger>
        rosconsole set <node> <logger> <level>
        ```

    - 使用`rosconsole`功能包的API：

        ```cpp
        // 设置日志输出的最低详细级别为WARN，详细级别>=WARN的日志会被输出
        if (ros::console::set_logger_level(ROSCONSOLE_DEFAULT_NAME, ros::console::levels::Warn)) {
          ros::console::notifyLoggerLevelsChanged();
        }
        ```

## 日志输出语法

1. 在使用`ROS_<verbosity level>`输出日志时，需要使用类似C中`printf()`的语法：

    ```cpp
    ROS_INFO("Hello %s", "World");
    ```

2. 在使用`ROS_<verbosity level>_STREAM`输出日志时，需要使用类似C++中`std::iostream`的语法：

    ```cpp
    ROS_INFO_STREAM("Hello " << "World");
    ```

## 参考

1. [roscpp/Overview/Logging-ROS Wiki](http://wiki.ros.org/roscpp/Overview/Logging)
2. [Verbosity Levels-ROS Wiki](http://wiki.ros.org/Verbosity%20Levels)
3. [ros中的日志输出级别-CSDN博客](https://blog.csdn.net/qq_42731705/article/details/123199541)
4. [ROS_INFO与ROS_INFO_STREAM-CSDN博客](https://blog.csdn.net/newbeixue/article/details/113842570)
