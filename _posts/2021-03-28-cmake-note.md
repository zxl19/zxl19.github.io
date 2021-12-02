---
layout: post
title: CMake学习笔记
date: 2021-03-28
author: zxl19
tags: [C++, CMake, Note]
comments: true
toc: true
pinned: true
---

我的CMake学习笔记及常用工程模板。

<!-- more -->

## 常用模板

### 非ROS工程

```cmake
cmake_minimum_required(VERSION 3.0)
project(project_name)

set(CMAKE_BUILD_TYPE "Release")                         # 编译模式：Debug/Release
set(CMAKE_CXX_STANDARD 11)                              # 指定C++标准：98、11、14、17、20
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)                   # 强制使用指定的C++标准
set(CMAKE_CXX_FLAGS "-std=c++11")                       # 针对C++的编译选项（经测试用此方式无法指定C++标准）
set(CMAKE_CXX_FLAGS_DEBUG "-O1 -Wall -g -pthread")      # 针对C++在Debug模式下的编译选项
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread")    # 针对C++在Release模式下的编译选项
# 采用如下方式也可，但是编译选项针对所有类型编译器
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

1. 使用`catkin_create_pkg`命令新建功能包，会自动生成`CMakeLists.txt`文件，其中包含格式说明；
2. 参考[ROS官方文档](http://wiki.ros.org/catkin/CMakeLists.txt)；
3. 参考[A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)、[LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)、[LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)、[LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)等算法；
4. 参考[hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)使用Nodelet；

## CMakeLists结构说明

### 基本结构

```cmake
cmake_minimum_required()
project()

# set()
# message()
# add_subdirectory()
# aux_source_directory()

find_package()

include_directories()
# link_directories()

# add_library()

add_executable()
# add_dependencies()
target_link_libraries()
```

### 结构说明

1. 推荐使用`set()`进行编译选项的设置，注意追加和覆盖的区别：

    ```cmake
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")   # 追加
    set(CMAKE_CXX_FLAGS "-O3")                      # 覆盖
    ```

2. `add_compile_options()`和`add_definitions()`针对所有编译器，应慎重使用；
3. 使用`add_subdirectory()`添加的子目录中需要存在`CMakeLists.txt`文件（内容可以为空）；
4. 推荐使用`aux_source_directory()`或`set()`构建源文件列表；
5. 纯头文件库只需`include_directories()`，例如：Eigen；
6. 在`find_package()`之后已能正确找到对应库路径，[不建议](http://wiki.ros.org/catkin/CMakeLists.txt)再使用`link_directories()`;
7. 自己定义的类和函数建议模块化，使用`add_library()`编译成静态库（推荐）；
8. 当定义的目标依赖另一个目标，确保在源码编译本目标之前，其他的目标已经被构建，使用`add_dependencies()`；

### 常用变量

| 变量名 | 含义 |
| :------ | :------|
| PROJECT_NAME | 工程名 |
| CMAKE_BUILD_TYPE | 编译模式 |
| CMAKE_CXX_STANDARD | 使用的C++标准 |
| CMAKE_CXX_STANDARD_REQUIRED | 是否强制使用指定的C++标准 |
| CMAKE_CXX_FLAGS | 编译参数 |
| CMAKE_CXX_FLAGS_DEBUG | Debug模式下的编译参数 |
| CMAKE_CXX_FLAGS_RELEASE | Release模式下的编译参数 |
| XXX_FOUND | XXX库是否找到 |
| XXX_VERSION | XXX库版本 |
| XXX_INCLUDE_DIRS | XXX库的头文件路径 |
| XXX_LIBRARY_DIRS | XXX库的链接路径 |
| XXX_LIBRARIES | XXX库的库名 |

## 学习资源

### 网站

1. [CMake Reference Documentation](https://cmake.org/cmake/help/latest/index.html)
2. [ttroy50/cmake-examples](https://github.com/ttroy50/cmake-examples)
3. [Effective Modern CMake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
4. [Cmake的应用与实践](https://www.bilibili.com/video/BV17J411m7o1)

### 书籍

1. [Modern CMake](http://cliutils.gitlab.io/modern-cmake/modern-cmake.pdf)
2. [Learning CMake](https://riptutorial.com/Download/cmake.pdf)
3. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)

## 参考

1. [Ceres CMakeLists-CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
2. [CMakeLists-简书](https://www.jianshu.com/p/95c744a5c6f1)
3. [指定C++编译标准1-Crascit](https://crascit.com/2015/03/28/enabling-cxx11-in-cmake/)
4. [指定C++编译标准2-腾讯云](https://cloud.tencent.com/developer/article/1741243)
5. [指定C++编译标准3-azmddy](https://azmddy.github.io/article/%E7%BC%96%E8%AF%91%E6%9E%84%E5%BB%BA/cmake-day-2.html)
6. [编译选项设置区别-CSDN博客](https://blog.csdn.net/10km/article/details/51731959)
7. [catkin/CMakeLists.txt](http://wiki.ros.org/catkin/CMakeLists.txt)
8. [HKUST-Aerial-Robotics/A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
9. [RobustFieldAutonomyLab/LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
10. [TixiaoShan/LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
11. [TixiaoShan/LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)
12. [koide3/hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)
13. [变量-简书](https://www.jianshu.com/p/1827cd86d576)
14. [CMake如何入门？-0xCCCCCCCC的回答-知乎](https://www.zhihu.com/question/58949190/answer/999701073)
15. [CMake和Modern CMake相关资料（不定期补充）-迦非喵的文章-知乎](https://zhuanlan.zhihu.com/p/205324774)
