---
layout: post
title: CMake学习笔记
date: 2021-03-28
author: zxl19
tags: [C++, CMake, Note]
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

set(CMAKE_BUILD_TYPE "Release")                         # 编译模式 Debug/Release
set(CMAKE_CXX_FLAGS "-std=c++11")                       # 针对C++的编译选项
set(CMAKE_CXX_FLAGS_DEBUG "-O1 -Wall -g -pthread")      # 针对C++在Debug模式下的编译选项
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread")    # 针对C++在Release模式下的编译选项
# 采用如下方式也可，但是编译选项针对所有编译器
# add_compile_options(-std=c++11 -O3 -Wall -g -pthread) # 不推荐

find_package(Eigen3 REQUIRED QUIET)
find_package(Ceres REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
find_package(OpenCV REQUIRED QUIET)
find_package(G2O REQUIRED QUIET)
find_package(GTSAM REQUIRED QUIET)

include_directories(
    include
    ${EIGEN3_INCLUDE_DIRS}
    ${CERES_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${G2O_INCLUDE_DIRS}
    ${GTSAM_INCLUDE_DIRS}
)

# link_directories(
#     include
#     ${CERES_LIBRARY_DIRS}
#     ${PCL_LIBRARY_DIRS}
#     ${OpenCV_LIBRARY_DIRS}
#     ${G2O_INCLUDE_DIRS}
#     ${GTSAM_LIBRARY_DIRS}
# )

add_executable(${PROJECT_NAME} src/main.cpp)
target_link_libraries(${PROJECT_NAME}
    ${CERES_LIBRARIES}
    ${PCL_LIBRARIES}
    ${OpenCV_LIBRARIES}
    ${G2O_LIBRARIES}
    ${GTSAM_LIBRARIES}
)
```

### ROS工程

1. [ROS官方文档](http://wiki.ros.org/catkin/CMakeLists.txt)
2. 参考[A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)、[LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)、[LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)、[LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)等算法。

## CMakeLists结构说明

```cmake
cmake_minimum_required()
project()

# set()
# add_subdirectory()
# aux_source_directory( , )

find_package( , )

include_directories()
# link_directories()

# add_library( , )

add_executable( , )
# add_dependencies( , )
target_link_libraries( , )
```

1. 推荐使用`set()`进行编译选项的设置；
2. 使用`add_subdirectory()`添加的子目录中需要存在`CMakeLists.txt`文件（内容可以为空）；
3. 推荐使用`set()`或`aux_source_directory()`将需要编译成库的`.cpp`文件名序列赋值给一个变量；
4. `add_compile_options()`和`add_definitions()`针对所有编译器，应慎重使用；
5. 纯头文件库只需`include_directories()`，例如：Eigen；
6. 在`find_package()`之后已能正确找到对应库路径，[不建议](http://wiki.ros.org/catkin/CMakeLists.txt)再使用`link_directories()`;
7. 自己定义的类和函数建议模块化，使用`add_library()`编译成静态库（推荐）；
8. 当定义的target依赖的另一个target，确保在源码编译本target之前，其他的target已经被构建，使用`add_dependencies()`；

## 参考

1. [Ceres CMakeLists-CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
2. [CMakeLists-简书](https://www.jianshu.com/p/95c744a5c6f1)
3. [编译选项设置区别-CSDN博客](https://blog.csdn.net/10km/article/details/51731959)
4. [CMake Reference Documentation](https://cmake.org/cmake/help/latest/index.html)
5. [Modern CMake](http://cliutils.gitlab.io/modern-cmake/)
6. [catkin/CMakeLists.txt](http://wiki.ros.org/catkin/CMakeLists.txt)
7. [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
8. [LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
9. [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
10. [LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)
11. [CMake 如何入门？-0xCCCCCCCC的回答-知乎](https://www.zhihu.com/question/58949190/answer/999701073)
12. [cmake-examples](https://github.com/ttroy50/cmake-examples)
13. [BV17J411m7o1](https://www.bilibili.com/video/BV17J411m7o1)
14. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)
