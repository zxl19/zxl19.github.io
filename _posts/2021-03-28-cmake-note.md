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

## CMake Hello World

1. CMake是Cross Platform Make的简称，是开源、跨平台的构建生成（build generator）工具；
2. CMake使用`CMakeLists.txt`配置文件控制编译过程，以C++编译过程为例：

    ```shell
    mkdir build
    cd build
    cmake ..    # CMake根据CMakeLists.txt配置文件生成Makefile文件
    make -j     # 编译器根据Makefile文件完成编译过程
    ```

## 常用模板

### 文件夹结构

```shell
.
├── app                     # 存放可执行文件，调用各个模块
├── build                   # 存放编译生成文件
├── cmake                   # 存放.cmake文件，查找依赖库
├── CMakeLists.txt          # 工程编译规则
├── config                  # 存放配置文件，硬件参数和软件参数分开保存
├── doc                     # 存放各个模块的开发文档
├── docker                  # 存放Docker镜像
├── include                 # 存放头文件，模块化
├── launch                  # 存放.launch文件，启动ROS功能包的各个节点
├── LICENSE                 # 开源协议
├── log                     # 存放日志文件
├── msg                     # 存放.msg文件，自定义ROS消息类型
├── package.xml             # 依赖的ROS功能包
├── README.md               # 工程说明文档
├── rviz_cfg                # 存放.rviz文件，配置Rviz可视化参数
├── scripts                 # 存放Python脚本，用于后处理和可视化
├── src                     # 存放源文件，模块化，编译成库
│   ├── algorithm           # 基础算法，滤波器、最近邻、RANSAC、样条曲线等
│   ├── CMakeLists.txt      # 添加子目录
│   ├── common              # 模块间共用的类、函数、常量等
│   ├── slam                # SLAM算法，激光、视觉、时间同步、位姿估计
│   └── ui                  # 可视化界面
├── test                    # 存放单元测试文件，测试各个模块
└── third_party             # 存放非本地安装的第三方库
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
# 工程配置
cmake_minimum_required()
project()
set()
unset()
include()

# 编译规则
find_package()
include_directories()
# link_directories()
add_library()
add_executable()
add_dependencies()
target_link_libraries()

# 辅助函数
option()
message()
add_definitions()
add_subdirectory()
aux_source_directory()
# add_compile_options()
install()

# 条件判断
if()
    # do something
elseif()
    # do something
else()
    # do something
endif()

# 循环遍历
foreach()
    # do something
endforeach()
```

### 常用命令

#### 基础说明

1. `CMakeLists.txt`文件使用`#`注释；
2. 功能函数名不区分大小写，支持大小写混用，但是推荐使用小写，可读性更好；
3. 功能函数参数中`<...>`表示必需项，`[...]`表示可选项，`|`表示或；
4. 变量名和字符串区分大小写；

#### 工程配置

1. `cmake_minimum_required()`用于指定CMake的最低版本，常用命令格式如下：

    ```cmake
    cmake_minimum_required(VERSION <major.minor>)
    ```

    示例：

    ```cmake
    cmake_minimum_required(VERSION 3.1.0)
    ```

2. `project()`用于指定工程名，常用命令格式如下：

    ```cmake
    project(<project_name>)
    ```

    示例：

    ```cmake
    project(HelloWorld)
    ```

3. `set()`用于定义变量并赋值，常用命令格式如下：

    ```cmake
    set(<variable> <value>)
    ```

    - CMake中，`X`表示变量名，`${X}`表示变量值；
    - 常用于设置编译选项，需要注意追加和覆盖的区别：

        ```cmake
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")   # 追加
        set(CMAKE_CXX_FLAGS "-O3")                      # 覆盖
        ```

4. `unset()`用于取消定义变量，常用命令格式如下：

    ```cmake
    unset(<variable>)
    ```

5. `include()`用于从文件或模块中加载并运行CMake代码，常用命令格式如下：

    ```cmake
    include(<file | module>)
    ```

    - 推荐将查找依赖库的部分写到`cmake`文件夹中的`packages.cmake`文件中，使用`include()`包含该文件即可：

        ```cmake
        include(cmake/packages.cmake)
        ```

    - `packages.cmake`文件示例：

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

#### 编译规则

1. `find_package()`用于查找外部工程并加载相关设置，外部工程通常为功能包或第三方依赖库，常用命令格式如下：

    ```cmake
    find_package(<package> [version] [QUIET] [REQUIRED]
                 [[COMPONENTS] [components...]])
    ```

2. `include_directories()`用于指定包含头文件目录，常用命令格式如下：

    ```cmake
    include_directories(<directory1> [directory2 ...])
    ```

    - 目录名被添加到`INCLUDE_DIRECTORIES`变量中；
    - 纯头文件库只需要`include_directories()`即可，例如：Eigen；

3. `link_directories()`用于指定链接时查找的库文件目录，常用命令格式如下：

    ```cmake
    link_directories(<directory1> [directory2 ...])
    ```

    - 在使用`find_package()`找到外部工程后会自动添加链接库信息，[不建议](http://wiki.ros.org/catkin/CMakeLists.txt)再使用`link_directories()`；

4. `add_library()`用于将指定的源文件编译成库，常用命令格式如下：

    ```cmake
    add_library(<name> [STATIC | SHARED | MODULE]
                <source1> [source2 ...])
    ```

    - 库的类型说明：

        | 库的类型 | 说明 |
        | :--- | :--- |
        | `STATIC` | 静态库，在链接时使用，在Linux系统中后缀为`.a`，在Windows系统中后缀为`.lib`，用空间换时间，全量更新 |
        | `SHARED` | 在程序运行时动态链接并加载，在Linux系统中被称为共享库，后缀为`.so`（shared object），在Windows系统中被称为动态链接库，后缀为`.dll`（dynamic link library），用时间换空间，增量更新 |
        | `MODULE` | 插件库，不链接，在程序运行时使用`dlopen`动态加载，使用较少 |

    - 如果未显式指定库的类型，将根据`BUILD_SHARED_LIBS`变量的值进行判断；
    - 常用于将各个模块分别编译成库：

        ```cmake
        add_library(${PROJECT_NAME}.algorithm SHARED
            foo1.cpp
            bar1.cpp
        )
        add_library(${PROJECT_NAME}.common SHARED
            foo2.cpp
            bar2.cpp
        )
        ```

5. `add_executable()`用于将指定的源文件编译成可执行文件，常用命令格式如下：

    ```cmake
    add_executable(<name>
                   <source1> [source2 ...])
    ```

6. `add_dependencies()`用于指定顶层编译目标（top-level targets）之间的依赖关系，常用命令格式如下：

    ```cmake
    add_dependencies(<target>
                     <dependency1> [dependency2 ...])
    ```

    - 顶层编译目标是由`add_library()`、`add_executable()`、`add_custom_target()`功能函数创建的编译目标，不包括`install()`功能函数生成的编译目标；
    - 当定义的顶层编译目标依赖其他顶层编译目标时，需要使用`add_dependencies()`指定依赖关系，保证在构建本目标之前，其他目标已构建完成；
    - 常用于`target_link_libraries()`之前；

7. `target_link_libraries()`用于指定编译目标需要链接的依赖库，常用命令格式如下：

    ```cmake
    target_link_libraries(<target>
                          <item1> [item2 ...])
    ```

    - 编译目标由`add_executable()`、`add_library()`功能函数创建；

#### 辅助函数

1. `option()`用于设置编译选项，常用语法如下：

    ```cmake
    option(<option_variable> "help string describing option"
           [initial_value])
    ```

    - 编译选项分为`ON`和`OFF`；
    - 如果不设置编译选项，初值默认为`OFF`；

2. `message()`用于输出消息，常用语法如下：

    ```cmake
    message([mode] "message to display" ...)
    ```

    - 消息类型说明：

        | 消息类型 | 说明 |
        | :--- | :--- |
        | `FATAL_ERROR` | CMake错误，停止处理和生成 |
        | `SEND_ERROR` | CMake错误，继续处理但跳过生成 |
        | `WARNING` | CMake警告，继续处理 |
        | `AUTHOR_WARNING` | CMake开发者警告，继续处理 |
        | `DEPRECATION` | 如果定义了`CMAKE_ERROR_DEPRECATED`或`CMAKE_WARN_DEPRECATED`，则输出CMake弃用错误或警告，否则无消息输出 |
        | `NOTICE`或未显式指定 | 打印到`stderr`的重要消息 |
        | `STATUS` | 一行以内的简明信息，供项目用户使用 |
        | `VERBOSE` | 详细信息，供项目用户使用 |
        | `DEBUG` | 详细信息，供项目开发者使用 |
        | `TRACE` | 细粒度信息，包含底层实现细节，临时使用，在项目发布、打包时删除 |

3. `add_definitions()`用于为编译指令添加`-D`开头的定义，常用语法如下：

    ```cmake
    add_definitions(-DFOO -DBAR ...)
    ```

    - 常用于实现条件编译：

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

    - 条件编译示例：

        ```cpp
        #ifdef FLAG_A
            // do something
        #elif FLAG_B
            // do something
        #else
            // do something
        #endif
        ```

4. `add_subdirectory()`用于添加子目录，常用语法如下：

    ```cmake
    add_subdirectory(<directory>)
    ```

    - 添加的子目录中需要存在`CMakeLists.txt`文件；

5. `aux_source_directory()`用于将指定目录中的源文件列表保存到变量中，常用语法如下：

    ```cmake
    aux_source_directory(<directory> <variable>)
    ```

    - 常用于构建源文件列表：

        ```cmake
        aux_source_directory(${PROJECT_NAME}/test TEST_SOURCES)
        ```

    - 也可以使用`set()`构建源文件列表：

        ```cmake
        set(TEST_SOURCES
            ${PROJECT_NAME}/test/test_algorithm.cpp
            ${PROJECT_NAME}/test/test_common.cpp
            ${PROJECT_NAME}/test/test_slam.cpp
        )
        ```

6. `add_compile_options()`用于设置编译选项，常用语法如下：

    ```cmake
    add_compile_options(<option1> [option2 ...])
    ```

    - `add_compile_options()`和`add_definitions()`针对所有编译器（包括C和C++），应慎重使用：

        ```cmake
        add_compile_options(-std=c++11 -Wall -pthread -fexceptions)     # 不推荐
        ```

7. `install()`用于定义安装规则，常用语法如下：

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
| `CMAKE_MODULE_PATH` | `include()`命令和`find_package()`命令查找CMake模块的路径 |
| `XXX_FOUND` | `XXX`库是否找到 |
| `XXX_VERSION` | `XXX`库版本 |
| `XXX_INCLUDE_DIRS` | `XXX`库的头文件路径 |
| `XXX_LIBRARY_DIRS` | `XXX`库的链接路径 |
| `XXX_LIBRARIES` | `XXX`库的库名 |

## 学习资源

### 网站

1. [CMake Reference Documentation](https://cmake.org/cmake/help/latest/index.html)
2. [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
3. [cmake使用教程](https://juejin.cn/post/6844903557183832078)
4. [基于VSCode和CMake实现C/C++开发丨Linux篇](https://www.bilibili.com/video/BV1fy4y1b7TC)
5. [Cmake的应用与实践](https://www.bilibili.com/video/BV17J411m7o1)

### GitHub

1. [ttroy50/cmake-examples](https://github.com/ttroy50/cmake-examples)
2. [Effective Modern CMake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
3. [kelthuzadx/EffectiveModernCppChinese](https://github.com/kelthuzadx/EffectiveModernCppChinese)
4. [TheLartians/ModernCppStarter](https://github.com/TheLartians/ModernCppStarter)
5. [cpp-best-practices/gui_starter_template](https://github.com/cpp-best-practices/gui_starter_template)
6. [BrightXiaoHan/CMakeTutorial](https://github.com/BrightXiaoHan/CMakeTutorial)
7. [district10/cmake-templates](https://github.com/district10/cmake-templates)
8. [nikolausmayer/cmake-templates](https://github.com/nikolausmayer/cmake-templates)

### 书籍

1. [Modern CMake](http://cliutils.gitlab.io/modern-cmake/modern-cmake.pdf)
2. [Learning CMake](https://riptutorial.com/Download/cmake.pdf)
3. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)

## 参考

1. [CMake](https://cmake.org)
2. [gaoxiang12/faster-lio](https://github.com/gaoxiang12/faster-lio)
3. [Ceres CMakeLists-CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
4. [CMakeLists-简书](https://www.jianshu.com/p/95c744a5c6f1)
5. [指定C++编译标准1-Stack Overflow](https://stackoverflow.com/questions/42834844/how-to-get-cmake-to-pass-either-std-c14-c1y-or-c17-c1z-based-on-gcc-vers)
6. [指定C++编译标准2-Crascit](https://crascit.com/2015/03/28/enabling-cxx11-in-cmake/)
7. [指定C++编译标准3-腾讯云](https://cloud.tencent.com/developer/article/1741243)
8. [指定C++编译标准4-azmddy](https://azmddy.github.io/article/IT%E5%9F%BA%E7%A1%80/%E6%9E%84%E5%BB%BA/CMake/cmake-day-2.html)
9. [Eigen内存对齐-卷儿的文章-知乎](https://zhuanlan.zhihu.com/p/349413376)
10. [catkin/CMakeLists.txt-ROS Wiki](http://wiki.ros.org/catkin/CMakeLists.txt)
11. [HKUST-Aerial-Robotics/A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
12. [RobustFieldAutonomyLab/LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
13. [TixiaoShan/LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)
14. [TixiaoShan/LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)
15. [koide3/hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)
16. [Cmake之深入理解find_package()的用法-希葛格的韩少君的文章-知乎](https://zhuanlan.zhihu.com/p/97369704)
17. [静态库、动态库、共享库的区别-博客园](https://www.cnblogs.com/sunsky303/p/7731911.html)
18. [add_dependencies()1-CSDN博客](https://blog.csdn.net/KingOfMyHeart/article/details/112983922)
19. [add_dependencies()2-CSDN博客](https://blog.csdn.net/zhizhengguan/article/details/118381772)
20. [add_dependencies()3-CSDN博客](https://blog.csdn.net/new9232/article/details/125831009)
21. [add_definitions()-CSDN博客](https://blog.csdn.net/fb_941219/article/details/107376017)
22. [编译选项设置区别-CSDN博客](https://blog.csdn.net/10km/article/details/51731959)
23. [变量1-简书](https://www.jianshu.com/p/1827cd86d576)
24. [变量2-CSDN博客](https://blog.csdn.net/juluwangriyue/article/details/123494008)
25. [变量3-CSDN博客](https://blog.csdn.net/wzj_110/article/details/116674655)
26. [CMake如何入门？-0xCCCCCCCC的回答-知乎](https://www.zhihu.com/question/58949190/answer/999701073)
27. [CMake和Modern CMake相关资料（不定期补充）-迦非喵的文章-知乎](https://zhuanlan.zhihu.com/p/205324774)
