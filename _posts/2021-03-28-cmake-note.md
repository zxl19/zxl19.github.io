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

### 文件夹结构

```shell
.
├── app             # 存放可执行文件，调用各个模块
├── build           # 存放编译生成文件
├── cmake           # 存放.cmake文件，查找依赖库
├── CMakeLists.txt  # 项目编译规则
├── config          # 存放配置文件，硬件参数和软件参数分开保存
├── doc             # 存放项目文档
├── docker          # 存放Docker镜像
├── include         # 存放头文件，模块化
├── launch          # 存放.launch文件，启动ROS功能包的各个节点
├── LICENSE         # 开源协议
├── log             # 存放日志文件
├── msg             # 存放.msg文件，自定义ROS消息类型
├── package.xml     # 依赖的ROS功能包
├── README.md       # 项目说明文档
├── rviz_cfg        # 存放.rviz文件，配置Rviz可视化参数
├── scripts         # 存放Python脚本，用于后处理和可视化
├── src             # 存放源文件，模块化
├── test            # 存放单元测试文件，测试各个模块
└── third_party     # 存放非本地安装的第三方库
```

### 非ROS工程

```cmake
cmake_minimum_required(VERSION 3.0)
project(project_name)

set(CMAKE_BUILD_TYPE "Release")                                 # 编译模式：Debug/Release
set(CMAKE_CXX_STANDARD 11)                                      # 指定C++标准：98、11、14、17、20
set(CMAKE_CXX_STANDARD_REQUIRED ON)                             # 强制使用指定的C++标准
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_FLAGS "-std=c++11 -Wall -pthread -fexceptions")   # 针对C++的编译选项（经测试用此方式无法指定C++标准，可能是由于CMake版本较高）
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} -O1 -g -ggdb")    # 针对C++在Debug模式下的编译选项
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -O3")           # 针对C++在Release模式下的编译选项
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)                           # 生成compile_commands.json文件

find_package(Eigen3 REQUIRED QUIET)
find_package(Ceres REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
find_package(OpenCV REQUIRED QUIET)
find_package(G2O REQUIRED QUIET)
find_package(GTSAM REQUIRED QUIET)
find_package(gflags REQUIRED QUIET)
find_package(glog REQUIRED QUIET)
find_package(gtest REQUIRED QUIET)
set(SOPHUS_INCLUDE_DIRS "${PROJECT_SOURCE_DIR}/third_party/Sophus")

include_directories(
    include
    ${EIGEN3_INCLUDE_DIRS}
    # ${CERES_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${G2O_INCLUDE_DIRS}
    ${GTSAM_INCLUDE_DIRS}
    ${SOPHUS_INCLUDE_DIRS}
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
    gflags
    glog
    gtest
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

# 常用命令
set()
include()
option()
message()
add_definitions()
add_subdirectory()
aux_source_directory()
# add_compile_options()

# 查找依赖库
find_package()
include_directories()

# link_directories()

add_library()

add_executable()
add_dependencies()
target_link_libraries()
```

### 结构说明

1. 推荐使用`set()`进行编译选项的设置，注意追加和覆盖的区别：

    ```cmake
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")   # 追加
    set(CMAKE_CXX_FLAGS "-O3")                      # 覆盖
    ```

2. 推荐将查找依赖库的部分写到`cmake`文件夹中的`packages.cmake`文件中，使用`include()`包含该文件即可：

    ```cmake
    include(cmake/packages.cmake)
    ```

    `packages.cmake`文件示例：

    ```cmake
    list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

    find_package(Eigen3 REQUIRED QUIET)
    find_package(PCL REQUIRED QUIET)

    include_directories(
        include
        ${EIGEN3_INCLUDE_DIRS}
        ${PCL_INCLUDE_DIRS}
    )
    ```

3. `add_definitions()`可用于定义预处理宏，实现条件编译：

    ```cmake
    option(USE_FLAG_A "Use Flag A" ON)
    option(USE_FLAG_B "Use Flag B" OFF)
    if(USE_FLAG_A)
        message("USING_FLAG_A")
        add_definitions(-DFLAG_A)   # 定义了名为FLAG_A的宏
    elseif(USE_FLAG_B)
        message("USING_FLAG_B")
        add_definitions(-DFLAG_B)   # 定义了名为FLAG_B的宏
    else()
        message("DEFAULT")
    endif()
    ```

    条件编译示例：

    ```cpp
    #ifdef FLAG_A
        // do something
    #elif FLAG_B
        // do something
    #else
        // do something
    #endif
    ```

4. 使用`add_subdirectory()`添加的子目录中需要存在`CMakeLists.txt`文件，内容可以为空；
5. 推荐使用`aux_source_directory()`或`set()`构建源文件列表；
6. `add_compile_options()`和`add_definitions()`针对所有编译器（包括C和C++），应慎重使用：

    ```cmake
    add_compile_options(-std=c++11 -Wall -pthread -fexceptions)     # 不推荐
    ```

7. 纯头文件库只需`include_directories()`，例如：Eigen；
8. 在`find_package()`之后已能正确找到对应库路径，[不建议](http://wiki.ros.org/catkin/CMakeLists.txt)再使用`link_directories()`；
9. 推荐将自己定义的类和函数模块化，使用`add_library()`编译成静态库，在编译可执行文件时直接链接相关静态库即可；
10. 当定义的目标依赖另一个目标，确保在源码编译本目标之前，其他的目标已经被构建，使用`add_dependencies()`；

### 常用变量

| 变量名 | 含义 |
| :------ | :------|
| `PROJECT_NAME` | 工程名 |
| `PROJECT_SOURCE_DIR` | 工程顶层目录 |
| `PROJECT_BINARY_DIR` | 工程编译目录 |
| `CMAKE_BUILD_TYPE` | 编译模式 |
| `CMAKE_CXX_STANDARD` | 使用的C++标准 |
| `CMAKE_CXX_STANDARD_REQUIRED` | 是否强制使用指定的C++标准 |
| `CMAKE_CXX_FLAGS` | 编译参数 |
| `CMAKE_CXX_FLAGS_DEBUG` | Debug模式下的编译参数 |
| `CMAKE_CXX_FLAGS_RELEASE` | Release模式下的编译参数 |
| `CMAKE_MODULE_PATH` | `.cmake`文件所在路径 |
| `XXX_FOUND` | `XXX`库是否找到 |
| `XXX_VERSION` | `XXX`库版本 |
| `XXX_INCLUDE_DIRS` | `XXX`库的头文件路径 |
| `XXX_LIBRARY_DIRS` | `XXX`库的链接路径 |
| `XXX_LIBRARIES` | `XXX`库的库名 |

## 学习资源

### 网站

1. [CMake Reference Documentation](https://cmake.org/cmake/help/latest/index.html)
2. [基于VSCode和CMake实现C/C++开发丨Linux篇](https://www.bilibili.com/video/BV1fy4y1b7TC)
3. [Cmake的应用与实践](https://www.bilibili.com/video/BV17J411m7o1)

### GitHub

1. [ttroy50/cmake-examples](https://github.com/ttroy50/cmake-examples)
2. [Effective Modern CMake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
3. [kelthuzadx/EffectiveModernCppChinese](https://github.com/kelthuzadx/EffectiveModernCppChinese)
4. [TheLartians/ModernCppStarter](https://github.com/TheLartians/ModernCppStarter)
5. [cpp-best-practices/gui_starter_template](https://github.com/cpp-best-practices/gui_starter_template)
6. [district10/cmake-templates](https://github.com/district10/cmake-templates)
7. [nikolausmayer/cmake-templates](https://github.com/nikolausmayer/cmake-templates)

### 书籍

1. [Modern CMake](http://cliutils.gitlab.io/modern-cmake/modern-cmake.pdf)
2. [Learning CMake](https://riptutorial.com/Download/cmake.pdf)
3. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)

## 参考

1. [gaoxiang12/faster-lio](https://github.com/gaoxiang12/faster-lio)
2. [Ceres CMakeLists-CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
3. [CMakeLists-简书](https://www.jianshu.com/p/95c744a5c6f1)
4. [指定C++编译标准1-Stack Overflow](https://stackoverflow.com/questions/42834844/how-to-get-cmake-to-pass-either-std-c14-c1y-or-c17-c1z-based-on-gcc-vers)
5. [指定C++编译标准2-Crascit](https://crascit.com/2015/03/28/enabling-cxx11-in-cmake/)
6. [指定C++编译标准3-腾讯云](https://cloud.tencent.com/developer/article/1741243)
7. [指定C++编译标准4-azmddy](https://azmddy.github.io/article/IT%E5%9F%BA%E7%A1%80/%E6%9E%84%E5%BB%BA/CMake/cmake-day-2.html)
8. [Eigen内存对齐-卷儿的文章-知乎](https://zhuanlan.zhihu.com/p/349413376)
9. [catkin/CMakeLists.txt-ROS Wiki](http://wiki.ros.org/catkin/CMakeLists.txt)
10. [HKUST-Aerial-Robotics/A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
11. [RobustFieldAutonomyLab/LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
12. [TixiaoShan/LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
13. [TixiaoShan/LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)
14. [koide3/hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)
15. [add_definitions()-CSDN博客](https://blog.csdn.net/fb_941219/article/details/107376017)
16. [编译选项设置区别-CSDN博客](https://blog.csdn.net/10km/article/details/51731959)
17. [变量1-简书](https://www.jianshu.com/p/1827cd86d576)
18. [变量2-CSDN博客](https://blog.csdn.net/juluwangriyue/article/details/123494008)
19. [变量3-CSDN博客](https://blog.csdn.net/wzj_110/article/details/116674655)
20. [CMake如何入门？-0xCCCCCCCC的回答-知乎](https://www.zhihu.com/question/58949190/answer/999701073)
21. [CMake和Modern CMake相关资料（不定期补充）-迦非喵的文章-知乎](https://zhuanlan.zhihu.com/p/205324774)
