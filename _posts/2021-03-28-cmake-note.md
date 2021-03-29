---
layout: post
title: CMake学习笔记
date: 2021-03-28
author: zxl19
tags: [C++, CMake]
comments: true
toc: true
pinned: false
---

我的CMake学习笔记及常用模板，供个人速查使用。

<!-- more -->

## 常用模板

### 非ROS工程

```cmake
cmake_minimum_required(VERSION 3.0)
project(project_name)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++11")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread")

find_package(Eigen3 REQUIRED QUIET)
find_package(Ceres REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
find_package(OpenCV REQUIRED QUIET)
find_package(GTSAM REQUIRED QUIET)

include_directories(
    include
    ${EIGEN3_INCLUDE_DIRS}
    ${CERES_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${GTSAM_INCLUDE_DIRS}
)

# link_directories(
#     include
#     ${CERES_LIBRARY_DIRS}
#     ${PCL_LIBRARY_DIRS}
#     ${OpenCV_LIBRARY_DIRS}
#     ${GTSAM_LIBRARY_DIRS}
# )

add_executable(${PROJECT_NAME} src/main.cpp)
target_link_libraries(${PROJECT_NAME}
    ${CERES_LIBRARIES}
    ${PCL_LIBRARIES}
    ${OpenCV_LIBRARIES}
    gtsam
)
```

### ROS工程

1. [ROS官方文档](http://wiki.ros.org/catkin/CMakeLists.txt)
2. 参考[A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)、[LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)、[LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)等算法。

## CMakeLists结构说明

```cmake
cmake_minimum_required()
project()

# set()

find_package( , )

include_directories()
# link_directories()

add_executable( , )
# add_dependencies( , )
target_link_libraries( , )
```

1. 纯头文件库只需`include_directories()`，例如：Eigen；
2. 在`find_package()`之后已能正确找到对应库路径，[不建议](http://wiki.ros.org/catkin/CMakeLists.txt)再使用`link_directories()`;
3. 自己定义的类和函数建议模块化，编译成静态库（推荐）；
4. 当定义的target依赖的另一个target，确保在源码编译本target之前，其他的target已经被构建，使用`add_dependencies()`；

## 参考

1. [CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
2. [catkin/CMakeLists.txt](http://wiki.ros.org/catkin/CMakeLists.txt)
3. [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
4. [LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
5. [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
6. [CMake 如何入门？-知乎](https://www.zhihu.com/question/58949190)
7. [cmake-examples](https://github.com/ttroy50/cmake-examples)
8. [BV17J411m7o1](https://www.bilibili.com/video/BV17J411m7o1)
9. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)
