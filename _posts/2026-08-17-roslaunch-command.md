---
layout: post
title: roslaunch命令行工具学习笔记
date: 2026-08-17
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

我的`roslaunch`命令行工具学习笔记。

<!-- more -->

## roslaunch Hello World

1. `roslaunch`命令行工具可以启动多个ROS节点，设置参数服务器上的参数，设置进程终止后是否自动重启；
2. `roslaunch`命令行工具使用的配置文件名后缀为`.launch`，使用XML语法；
3. `roscore`命令是`roslaunch`命令的特化，用于启动ROS核心系统，包括ROS Master、参数服务器、rosout；
4. 如果`roslaunch`命令检测到`roscore`命令未在运行，会自动启动`roscore`；
5. 由于存在竞态条件，不能使用`roslaunch`命令保证`roscore`只有一个单例（Singleton）实例；
6. 语法说明：

    ```shell
    roslaunch [options] [package] <filename> [arg_name:=value...]
    roslaunch [options] <filename> [<filename>...] [arg_name:=value...]
    ```

7. 显示帮助信息：

    ```shell
    roslaunch -h
    ```

## 教程

1. [Roslaunch tips for large projects-ROS Wiki](https://wiki.ros.org/roslaunch/Tutorials/Roslaunch%20tips%20for%20larger%20projects)
2. [How to Roslaunch Nodes in Valgrind or GDB-ROS Wiki](https://wiki.ros.org/roslaunch/Tutorials/Roslaunch%20Nodes%20in%20Valgrind%20or%20GDB)
3. [How to profile roslaunch nodes-ROS Wiki](https://wiki.ros.org/roslaunch/Tutorials/Profiling%20roslaunch%20nodes)

## 参考

1. [roslaunch-ROS Wiki](https://wiki.ros.org/roslaunch)
2. [roslaunch/XML-ROS Wiki](https://wiki.ros.org/roslaunch/XML)
3. [roslaunch/Commandline Tools-ROS Wiki](https://wiki.ros.org/roslaunch/Commandline%20Tools)
