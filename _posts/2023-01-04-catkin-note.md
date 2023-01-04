---
layout: post
title: Catkin学习笔记
date: 2023-01-04
author: zxl19
tags: [C++, Catkin, CMake, Note]
comments: true
toc: true
pinned: false
---

我的Catkin学习笔记。

<!-- more -->

## Catkin Hello World

1. ROS在CMake的基础上开发了`catkin_make`工具[^1]，用于高效编译多个相互依赖但是分别开发的功能包，以C++编译过程为例：

    ```shell
    catkin_make
    ```

    相当于执行了以下命令：

    ```shell
    mkdir build
    cd build
    cmake ../src -DCATKIN_DEVEL_SPACE=../devel -DCMAKE_INSTALL_PREFIX=../install
    make -j<number of cores> -l<number of cores> [optional target, e.g. install]
    ```

    [^1]: The name catkin comes from the tail-shaped flower cluster found on willow trees -- a reference to Willow Garage where catkin was created. -- catkin conceptual overview

    - 优点：
        - 相比分别编译各个功能包节省了编译生成文件占据的空间；
        - 可以并行编译多个功能包，即使它们是相互依赖的；
    - 缺点：
        - 修改一个功能包的`CMakeLists.txt`文件后需要重新编译工作空间中的所有功能包；
        - 没有故障隔离（fault isolation）机制，没有依赖项的功能包中的编译错误会阻止所有功能包的编译；
        - 功能包之间的编译目标名以及CMake变量名可能存在冲突；
        - 需要显式声明功能包之间的依赖关系；
        - 要求功能包都是由`catkin_make`工具构建的；

2. 在`catkin_make`工具的基础上开发了`catkin_make_isolated`工具，用于隔离编译各个功能包，解决了`catkin_make`工具中存在的上述问题，但是无法并行编译多个功能包，即使它们是相互独立的；
3. 在`catkin_make_isolated`工具的基础上开发了`catkin`工具，通过`catkin build`命令按照拓扑顺序隔离编译各个功能包，同时并行编译相互独立的功能包；

## Catkin工作流程

```shell
source /opt/ros/melodic/setup.bash          # Source ROS melodic to use Catkin
mkdir -p ~/catkin_ws/src                    # Make a new workspace and source space
cd ~/catkin_ws                              # Navigate to the workspace root
catkin init                                 # Initialize it with a hidden marker file
cd ~/catkin_ws/src                          # Navigate to the source space
catkin create pkg pkg_a                     # Populate the source space with packages...
catkin create pkg pkg_b
catkin create pkg pkg_c --catkin-deps pkg_a
catkin create pkg pkg_d --catkin-deps pkg_a pkg_b
catkin list                                 # List the packages in the workspace
catkin build                                # Build all packages in the workspace
source ~/catkin_ws/devel/setup.bash         # Load the workspace's environment
catkin clean                                # Clean all the build products
```

## 参考

1. [catkin-ROS Wiki](http://wiki.ros.org/catkin)
2. [ros中的catkin是什么东西？-锦城牛仔的回答-知乎](https://www.zhihu.com/question/63306098/answer/2318990933)
3. [ros中的catkin是什么东西？-MQLhhhh的回答-知乎](https://www.zhihu.com/question/63306098/answer/605358268)
4. [Catkin Command Line Tools](https://catkin-tools.readthedocs.io/en/latest/)
5. [catkin/catkin_tools](https://github.com/catkin/catkin_tools)
