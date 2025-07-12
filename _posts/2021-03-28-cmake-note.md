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

我的CMake学习笔记及常用工程模板。

<!-- more -->

## CMake Hello World

1. CMake是Cross Platform Make的简称，是开源、跨平台的构建生成（build generator）工具；
2. CMake工程的构建方式可以分为内部构建（in-source build）和外部构建（out-of-source build）两种，外部构建使用`build`文件夹存储编译生成文件，使源代码与编译生成文件分离，便于维护，推荐使用外部构建；
3. CMake使用`CMakeLists.txt`配置文件控制编译过程，以C++编译过程为例：

    ```shell
    mkdir build
    cd build    # 外部构建
    cmake ..    # CMake根据CMakeLists.txt配置文件生成Makefile文件
    make -j     # 编译器根据Makefile文件完成编译过程
    ```

    - `-j`选项用于指定并行任务数，一般设置为CPU物理核心数`$(nproc)`；
    - 如果任务中存在大量I/O等待，可以设置为CPU物理核心数加一；
    - 如果不指定并行任务数，表示不限制，可能导致内存占用过多，编译过程卡死，需要谨慎使用；

4. CMake提供了图形化交互界面CMake GUI，使用以下命令安装并运行：

    ```shell
    # 安装
    sudo apt install cmake-qt-gui
    # 运行
    cmake-gui
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

1. 外部使用的头文件放在`include`文件夹中；
2. 内部使用的头文件放在`src`文件夹中，与同名源文件放在同一目录下；

### CMakeLists

#### 非ROS工程

```cmake
cmake_minimum_required(VERSION 3.1.0)
project(project_name)

set(CMAKE_BUILD_TYPE "Release")                                 # 编译模式：Debug/Release
set(CMAKE_CXX_STANDARD 11)                                      # 指定C++标准：98、11、14、17、20
set(CMAKE_CXX_STANDARD_REQUIRED ON)                             # 强制使用指定的C++标准（CMake 3.1以上支持）
set(CMAKE_CXX_EXTENSIONS OFF)                                   # 禁用编译器扩展
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

#### ROS工程

1. 使用`catkin_create_pkg`命令新建功能包，会自动生成`CMakeLists.txt`文件，其中包含格式说明；
2. 参考[ROS官方文档](http://wiki.ros.org/catkin/CMakeLists.txt)；
3. 参考[HKUST-Aerial-Robotics/A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)、[RobustFieldAutonomyLab/LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)、[TixiaoShan/LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)、[TixiaoShan/LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)等算法；
4. 参考[koide3/hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)使用Nodelet；
5. 参考[facontidavide/LeGO-LOAM-BOR](https://github.com/facontidavide/LeGO-LOAM-BOR)、[koide3/LeGO-LOAM-BOR](https://github.com/koide3/LeGO-LOAM-BOR)实现离线和在线两种模式；
6. 参考[知乎回答](https://www.zhihu.com/question/553199862/answer/2672914532)进行正向设计；

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
target_include_directories()

# 辅助函数
option()
message()
add_definitions()
add_subdirectory()
aux_source_directory()
add_compile_options()
install()
enable_testing()
add_test()

# 条件判断
if()
    # do something
elseif()
    # do something
else()
    # do something
endif()

# 循环遍历
## for循环
foreach()
    # do something
endforeach()
## while循环
while()
    # do something
endwhile()
```

### 常用变量

| 变量名 | 含义 |
| :------ | :------|
| `PROJECT_NAME` | 工程名 |
| `PROJECT_SOURCE_DIR` | 工程顶层目录 |
| `PROJECT_BINARY_DIR` | 工程编译目录 |
| `CMAKE_VERSION` | CMake版本 |
| `CMAKE_SOURCE_DIR` | 工程顶层目录 |
| `CMAKE_BINARY_DIR` | 工程编译目录 |
| `CMAKE_CURRENT_SOURCE_DIR` | 当前处理`CMakeLists.txt`文件的所在目录 |
| `CMAKE_CURRENT_BINARY_DIR` | 当前处理`CMakeLists.txt`文件的编译目录 |
| `CMAKE_BUILD_TYPE` | 编译模式 |
| `CMAKE_CXX_STANDARD` | 使用的C++标准 |
| `CMAKE_CXX_STANDARD_REQUIRED` | 是否强制使用指定的C++标准 |
| `CMAKE_CXX_FLAGS` | 编译参数 |
| `CMAKE_CXX_FLAGS_DEBUG` | Debug模式下的编译参数 |
| `CMAKE_CXX_FLAGS_RELEASE` | Release模式下的编译参数 |
| `CMAKE_MODULE_PATH` | `include()`命令和`find_package()`命令查找CMake模块的路径 |
| `CMAKE_INSTALL_PREFIX` | `install()`命令使用相对路径安装时的路径前缀 |
| `XXX_DIR` | `XXX`库的查找路径 |
| `XXX_FOUND` | `XXX`库是否找到 |
| `XXX_VERSION` | `XXX`库版本 |
| `XXX_INCLUDE_DIRS` | `XXX`库的头文件路径 |
| `XXX_LIBRARY_DIRS` | `XXX`库的链接路径 |
| `XXX_LIBRARIES` | `XXX`库的库文件名 |

### 常用命令

#### 基础说明

1. `CMakeLists.txt`文件使用`#`注释；
2. 功能函数名不区分大小写，支持大小写混用，但是推荐使用小写，可读性更好；
3. 功能函数参数中`<...>`表示必需项，`[...]`表示可选项，`|`表示或；
4. 变量名和字符串区分大小写，推荐使用大写，可读性更好；

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

    - `find_package()`具有三种模式：
        - Module模式：
            - 搜索`Find<PackageName>.cmake`文件；
            - 首先在`CMAKE_MODULE_PATH`中查找，其次在CMake安装的`Find Modules`中查找；
            - 搜索的文件通常由操作系统或者CMake提供，启发式（heuristic）搜索，容易过时；
        - Config模式：
            - 搜索`<lowercasePackageName>-config.cmake`或`<PackageName>Config.cmake`文件；
            - 如果指定了版本，则搜索`<lowercasePackageName>-config-version.cmake`或`<PackageName>ConfigVersion.cmake`文件；
            - 搜索的文件通常由第三方依赖库提供，作为第三方依赖库的一部分安装，包含详细信息，不需要启发式搜索，相比于Module模式更加可靠，
        - FetchContent重定向模式：
            - 使用`FetchContent`模块；
            - 3.24版本新增；
    - 在安装第三方依赖库时，相关`.cmake`文件的路径会写入`XXX_DIR`环境变量中，`find_package()`通过查找`XXX_DIR`环境变量的值来查找上述`.cmake`文件，进而查找库文件的位置；
    - 如果第三方依赖库未安装到系统中，可以对于`XXX_DIR`变量手动赋值，再使用`find_package()`查找第三方依赖库，常用于查找`third_party`文件夹中非本地安装的第三方依赖库；

2. `include_directories()`用于指定包含头文件目录，常用命令格式如下：

    ```cmake
    include_directories(<directory1> [directory2 ...])
    ```

    - 目录名被添加到`INCLUDE_DIRECTORIES`变量中；
    - 如果使用相对路径，认为其相对于`CMAKE_CURRENT_SOURCE_DIR`；
    - 纯头文件库只需要`include_directories()`即可，例如：Eigen；

3. `link_directories()`用于指定链接时查找的库文件目录，常用命令格式如下：

    ```cmake
    link_directories(<directory1> [directory2 ...])
    ```

    - 如果使用相对路径，认为其相对于`CMAKE_CURRENT_SOURCE_DIR`；
    - CMake和ROS均**不建议**使用`link_directories()`，因为使用`find_package()`已经能够获得外部工程的完整绝对路径，通常可以直接使用`target_link_libraries()`；

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
        add_library(${PROJECT_NAME}.slam SHARED
            foo3.cpp
            bar3.cpp
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

    - 顶层编译目标是由`add_library()`、`add_executable()`、`add_custom_target()`命令创建的编译目标，不包括`install()`命令生成的编译目标；
    - 当定义的顶层编译目标依赖其他顶层编译目标时，需要使用`add_dependencies()`指定依赖关系，保证在构建本目标之前，本目标依赖的其他目标已构建完成；
    - 常用于`target_link_libraries()`之前；

7. `target_link_libraries()`用于指定编译目标需要链接的依赖库，常用命令格式如下：

    ```cmake
    target_link_libraries(<target>
                          <item1> [item2 ...])
    ```

    - 编译目标由`add_executable()`、`add_library()`命令创建；
    - 建议在使用`find_package()`找到依赖库后使用`${XXX_LIBRARIES}`的形式链接相关库文件；
    - 可以使用`-lfoo`或`foo.lib`的形式指定库文件名，会搜索并链接库文件`libfoo.so`，常用于处理`libfoo.so`作为依赖库的依赖库时出现的未定义符号问题，一般情况下不建议使用；

8. `target_include_directories()`用于指定编译目标需要包含的头文件目录，常用命令格式如下：

    ```cmake
    target_include_directories(<target>
                               <PRIVATE | INTERFACE | PUBLIC>
                               <item1> [item2 ...]
    )
    ```

    - 编译目标由`add_executable()`、`add_library()`命令创建；
    - 参数说明：

        | 参数 | 说明 |
        | :--- | :--- |
        | `PRIVATE` | 私有，仅在编译目标内部使用，外部无法通过编译目标使用 |
        | `INTERFACE` | 接口，编译目标内部不使用，外部通过编译目标使用 |
        | `PUBLIC` | 公开，编译目标内部使用，外部通过编译目标使用，`PUBLIC = PRIVATE + INTERFACE` |

    - 如果使用相对路径，认为其相对于`CMAKE_CURRENT_SOURCE_DIR`；
    - `include_directories()`包含的头文件目录可以被工程中的所有文件访问，但是`target_include_directories()`只能被指定的编译目标访问；
    - 如果工程中存在不同目录下的同名头文件，为了避免混淆，建议使用`target_include_directories()`；

#### 辅助函数

1. `option()`用于设置编译选项，常用语法如下：

    ```cmake
    option(<variable> "help string describing option"
           [value])
    ```

    - 编译选项是布尔值，分为`ON`和`OFF`；
    - 如果未显式指定编译选项的值，默认为`OFF`；

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

    - 常用于定义宏，实现条件编译：

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

4. `add_subdirectory()`用于添加子目录到工程中进行构建，常用语法如下：

    ```cmake
    add_subdirectory(<directory>)
    ```

    - 添加的子目录中需要存在`CMakeLists.txt`文件；
    - 如果使用相对路径，认为其相对于`CMAKE_CURRENT_SOURCE_DIR`；

5. `aux_source_directory()`用于将指定目录中的源文件列表保存到变量中，常用语法如下：

    ```cmake
    aux_source_directory(<directory> <variable>)
    ```

    - 如果使用相对路径，认为其相对于`CMAKE_CURRENT_SOURCE_DIR`；
    - 常用于构建源文件列表：

        ```cmake
        aux_source_directory(${PROJECT_NAME}/test TEST_SOURCES)
        ```

        - 需要注意的是，源文件列表不会随着目录中的源文件增加而自动更新，需要手动重新运行CMake来更新源文件列表；

    - 也可以使用`set()`构建源文件列表：

        ```cmake
        set(TEST_SOURCES
            ${PROJECT_NAME}/test/test_algorithm.cpp
            # ${PROJECT_NAME}/test/test_common.cpp
            ${PROJECT_NAME}/test/test_slam.cpp
        )
        ```

        - 可以直观看出源文件列表的内容，并且可以控制添加到源文件列表中的源文件；
        - 修改`CMakeLists.txt`文件后必须重新运行CMake，可以保证源文件列表的及时更新；

6. `add_compile_options()`用于设置编译选项，常用语法如下：

    ```cmake
    add_compile_options(<option1> [option2 ...])
    ```

    - `add_compile_options()`和`add_definitions()`针对所有编译器（包括C和C++），应慎重使用：

        ```cmake
        add_compile_options(-std=c++11 -Wall -pthread -fexceptions)     # 不推荐
        ```

    - 常用于屏蔽编译器警告，一般情况下只对于第三方依赖库使用，对于内部代码建议修复编译警告：

        ```cmake
        -w          # 屏蔽所有警告
        -Wxxx       # 启用特定警告
        -Wno-xxx    # 屏蔽特定警告
        # 示例
        -Wall       # 启用所有标准警告
        -Wno-all    # 屏蔽所有标准警告
        ```

7. `install()`用于定义安装规则，包括编译目标、文件、目录等；

    - 安装编译目标的常用语法如下：

        ```cmake
        install(TARGETS <target1> [target2 ...]
                <ARCHIVE | LIBRARY | RUNTIME> DESTINATION <directory>
        )
        ```

        - 编译目标由`add_executable()`、`add_library()`命令创建；
        - 参数说明：

            | 参数 | 说明 |
            | :--- | :--- |
            | `ARCHIVE` | `STATIC`类型的库 |
            | `LIBRARY` | `SHARED`和`MODULE`类型的库 |
            | `RUNTIME` | 可执行文件 |

        - 如果使用相对路径，认为其相对于`CMAKE_INSTALL_PREFIX`：

            - 在Unix系统中，`CMAKE_INSTALL_PREFIX`默认值为`/usr/local`；
            - 在Windows系统中，`CMAKE_INSTALL_PREFIX`默认值为`C:/Program Files/${PROJECT_NAME}`；

        - 示例：

            ```cmake
            install(TARGETS ${PROJECT_NAME}.algorithm
                    LIBRARY DESTINATION lib
                    ARCHIVE DESTINATION lib
                    RUNTIME DESTINATION bin
            )
            install(TARGETS ${PROJECT_NAME}.common
                    LIBRARY DESTINATION lib
                    ARCHIVE DESTINATION lib
                    RUNTIME DESTINATION bin
            )
            install(TARGETS ${PROJECT_NAME}.slam
                    LIBRARY DESTINATION lib
                    ARCHIVE DESTINATION lib
                    RUNTIME DESTINATION bin
            )
            ```

    - 安装文件的常用语法如下：

        ```cmake
        install(<FILES | PROGRAMS> <file1> [file2 ...]
                DESTINATION <directory>
        )
        ```

    - 安装目录的常用语法如下：

        ```cmake
        install(DIRECTORY <directory1> [directory2 ...]
                DESTINATION <directory3>
                [FILES_MATCHING [PATTERN <pattern> | REGEX <regex>]]
        )
        ```

        - 可以使用模糊匹配或正则表达式查找指定的文件名；
        - 示例：

            ```cmake
            install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/third_party/Sophus/"
                    DESTINATION "include/Sophus"
                    FILES_MATCHING
                    PATTERN "*.h"
                    PATTERN "*.hpp"
            )
            ```

8. `enable_testing()`用于启用当前目录下的所有测试，供`CTest`模块使用，常用语法如下：

    ```cmake
    enable_testing()
    ```

    - `CTest`模块希望在工程编译目录下找到测试文件，因此本命令应位于工程顶层`CMakeLists.txt`文件中；
    - 如果已经在`CMakeLists.txt`文件中包含`CTest`模块，则`enable_testing()`命令会被自动调用：

        ```cmake
        include(CTest)
        ```

9. `add_test()`用于生成测试文件，供`CTest`模块使用，常用语法如下：

    ```cmake
    add_test(NAME <name>
             COMMAND <command> [<arg> ...]
    )
    ```

#### 条件判断

##### 常用语法

`if()`用于根据条件判断执行不同的命令，常用语法如下：

```cmake
if(<condition>)
    <command>
elseif(<condition>)     # optional block, can be repeated
    <command>
else()                  # optional block
    <command>
endif()
```

##### 表达式优先级

1. 括号`()`;
2. 一元测试（unary test）：

    - `EXISTS`：文件或目录是否存在；
    - `COMMAND`：是否为可调用的命令、宏、函数；
    - `DEFINED`：变量是否定义；

3. 二元测试（binary test）：

    - `EQUAL`：等于；
    - `LESS`：小于；
    - `LESS_EQUAL`：小于等于；
    - `GREATER`：大于；
    - `GREATER_EQUAL`：大于等于；
    - `STREQUAL`：字符串等于；
    - `STRLESS`：字符串小于；
    - `STRLESS_EQUAL`：字符串小于等于；
    - `STRGREATER`：字符串大于；
    - `STRGREATER_EQUAL`：字符串大于等于；
    - `VERSION_EQUAL`：版本等于；
    - `VERSION_LESS`：版本小于；
    - `VERSION_LESS_EQUAL`：版本小于等于；
    - `VERSION_GREATER`：版本大于；
    - `VERSION_GREATER_EQUAL`：版本大于等于；
    - `PATH_EQUAL`：路径等于；
    - `MATCHES`：匹配正则表达式结果；

4. 一元逻辑运算符（unary logical operator）：

    - `NOT`：逻辑非；

5. 二元逻辑运算符（binary logical operator），从左到右，无短路现象：

    - `AND`：逻辑与；
    - `OR`：逻辑或；

##### 表达式类型说明

1. 常量：

    - 返回真：`1`、`ON`、`YES`、`TRUE`、`Y`、非零数（包括浮点数）；
    - 返回假：`0`、`OFF`、`NO`、`FALSE`、`N`、`IGNORE`、`NOTFOUND`、空字符串、后缀为`-NOTFOUND`；

2. 变量：

    - 返回真：**变量值**为真常量；
    - 返回假：**变量值**为假常量，或者变量未被定义；
    - 宏定义和环境变量不是变量，会返回假；

3. 字符串：

    - 带引号的字符串始终返回假，除非字符串的值是真常量；

#### 循环遍历

1. 循环体中的命令在循环中会被记录，在循环结束后一起执行；
2. `foreach()`用于对列表中的每一个值执行相同的命令，常用语法如下：

    ```cmake
    foreach(<loop_variable> <variable_list>)
        <command>
    endforeach([loop_variable])
    ```

    - 示例：

        ```cmake
        foreach(test_src ${TEST_SOURCES})
            add_executable(${test_src} ${test_src}.cpp)
            target_link_libraries(${test_src}
                ${PROJECT_NAME}.algorithm
                ${PROJECT_NAME}.common
                ${PROJECT_NAME}.slam
            )
            add_test(${test_src} ${test_src})
        endforeach(test_src)
        ```

3. `while()`用于在表达式的值为真时执行相同的命令，常用语法如下：

    ```cmake
    while(<condition>)
        <command>
    endwhile([condition])
    ```

## 资料

### 网站

1. [CMake Reference Documentation](https://cmake.org/cmake/help/latest/index.html)
2. [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
3. [GCC online documentation](https://gcc.gnu.org/onlinedocs/)
4. [CMake 3.25 中文-Runebooks.dev](https://runebook.dev/zh-CN/docs/cmake/-index-)
5. [CMake菜谱（CMake Cookbook中文版）](https://www.bookstack.cn/books/CMake-Cookbook)
6. [cmake使用教程](https://juejin.cn/post/6844903557183832078)
7. [基于VSCode和CMake实现C/C++开发丨Linux篇](https://www.bilibili.com/video/BV1fy4y1b7TC)
8. [Cmake的应用与实践](https://www.bilibili.com/video/BV17J411m7o1)

### GitHub

1. [ttroy50/cmake-examples](https://github.com/ttroy50/cmake-examples)
2. [mbinna/effective_modern_cmake.md](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
3. [TheLartians/ModernCppStarter](https://github.com/TheLartians/ModernCppStarter)
4. [cpp-best-practices/gui_starter_template](https://github.com/cpp-best-practices/gui_starter_template)
5. [dev-cafe/cmake-cookbook](https://github.com/dev-cafe/cmake-cookbook)
6. [filipdutescu/modern-cpp-template](https://github.com/filipdutescu/modern-cpp-template)
7. [xiaoweiChen/CMake-Cookbook](https://github.com/xiaoweiChen/CMake-Cookbook)
8. [pr0g/cmake-examples](https://github.com/pr0g/cmake-examples)
9. [BrightXiaoHan/CMakeTutorial](https://github.com/BrightXiaoHan/CMakeTutorial)
10. [pabloariasal/modern-cmake-sample](https://github.com/pabloariasal/modern-cmake-sample)
11. [district10/cmake-templates](https://github.com/district10/cmake-templates)
12. [Modern-CMake-CN/Modern-CMake-zh_CN](https://github.com/Modern-CMake-CN/Modern-CMake-zh_CN)
13. [PacktPublishing/CMake-Cookbook](https://github.com/PacktPublishing/CMake-Cookbook)
14. [mortennobel/CMake-Cheatsheet](https://github.com/mortennobel/CMake-Cheatsheet)
15. [mariokonrad/cmake-cheatsheet](https://github.com/mariokonrad/cmake-cheatsheet)
16. [nikolausmayer/cmake-templates](https://github.com/nikolausmayer/cmake-templates)

### 书籍

1. [Modern CMake](http://cliutils.gitlab.io/modern-cmake/modern-cmake.pdf)
2. [Learning CMake](https://riptutorial.com/Download/cmake.pdf)
3. [CMake Practice](http://file.ncnynl.com/ros/CMake%20Practice.pdf)

## 参考

1. [CMake](https://cmake.org)
2. [GCC](https://gcc.gnu.org)
3. [内部构建和外部构建-CSDN博客](https://blog.csdn.net/sandalphon4869/article/details/100589747)
4. [简单理解：CPU物理数，核心数，线程数，进程，线程，协程，并发，并行的概念-不是罗罗的文章-知乎](https://zhuanlan.zhihu.com/p/490318618)
5. [gaoxiang12/faster-lio](https://github.com/gaoxiang12/faster-lio)
6. [c++的.h和cpp，放在相同目录下好，还是顶层就用include,src分开好？-icon-meh的回答-知乎](https://www.zhihu.com/question/8622503673/answer/72070024144)
7. [c++的.h和cpp，放在相同目录下好，还是顶层就用include,src分开好？-柳翔天的回答-知乎](https://www.zhihu.com/question/8622503673/answer/71362286271)
8. [Ceres CMakeLists-CSDN博客](https://blog.csdn.net/sinat_28752257/article/details/82758546)
9. [CMakeLists-简书](https://www.jianshu.com/p/95c744a5c6f1)
10. [配置优化器：Debug与Release版本-FrankDellaert的文章-知乎](https://zhuanlan.zhihu.com/p/21403075327)
11. [Options That Control Optimization-GCC](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)
12. [Options for Debugging Your Program-GCC](https://gcc.gnu.org/onlinedocs/gcc/Debugging-Options.html)
13. [指定C++编译标准1-Stack Overflow](https://stackoverflow.com/questions/42834844/how-to-get-cmake-to-pass-either-std-c14-c1y-or-c17-c1z-based-on-gcc-vers)
14. [指定C++编译标准2-Crascit](https://crascit.com/2015/03/28/enabling-cxx11-in-cmake/)
15. [指定C++编译标准3-腾讯云](https://cloud.tencent.com/developer/article/1741243)
16. [指定C++编译标准4-azmddy](https://azmddy.github.io/article/IT%E5%9F%BA%E7%A1%80/%E6%9E%84%E5%BB%BA/CMake/cmake-day-2.html)
17. [Eigen内存对齐-卷儿的文章-知乎](https://zhuanlan.zhihu.com/p/349413376)
18. [catkin/CMakeLists.txt-ROS Wiki](http://wiki.ros.org/catkin/CMakeLists.txt)
19. [SLAＭ算法开发中，Ｃ++编程+多节点，如何调试和优化算法比较方便呢？正确的调试方法是什么？-半闲居士的回答-知乎](https://www.zhihu.com/question/553199862/answer/2672914532)
20. [cmake-developer](https://cmake.org/cmake/help/latest/manual/cmake-developer.7.html)
21. [变量1-博客园](https://www.cnblogs.com/narjaja/p/9533174.html)
22. [变量2-掘金](https://juejin.cn/post/6998055558741753893)
23. [变量3-CSDN博客](https://blog.csdn.net/juluwangriyue/article/details/123494008)
24. [变量4-CSDN博客](https://blog.csdn.net/wzj_110/article/details/116674655)
25. [变量5-简书](https://www.jianshu.com/p/1827cd86d576)
26. [Cmake之深入理解find_package()的用法-希葛格的韩少君的文章-知乎](https://zhuanlan.zhihu.com/p/97369704)
27. [cmake find_package路径详解-豌豆的文章-知乎](https://zhuanlan.zhihu.com/p/50829542)
28. [find_package()1-CSDN博客](https://blog.csdn.net/zhanghm1995/article/details/105466372)
29. [find_package()2-CSDN博客](https://blog.csdn.net/qq_41035283/article/details/122469466)
30. [Ceres_DIR1-CSDN博客](https://blog.csdn.net/qq_15642411/article/details/83656855)
31. [Ceres_DIR2-CSDN博客](https://blog.csdn.net/DumpDoctorWang/article/details/84587331)
32. [OpenCV_DIR-CSDN博客](https://blog.csdn.net/zkp_987/article/details/119913049)
33. [静态库、动态库、共享库的区别-博客园](https://www.cnblogs.com/sunsky303/p/7731911.html)
34. [add_dependencies()1-CSDN博客](https://blog.csdn.net/KingOfMyHeart/article/details/112983922)
35. [add_dependencies()2-CSDN博客](https://blog.csdn.net/zhizhengguan/article/details/118381772)
36. [add_dependencies()3-CSDN博客](https://blog.csdn.net/new9232/article/details/125831009)
37. [cmake：target_**中的PUBLIC，PRIVATE，INTERFACE-大川搬砖的文章-知乎](https://zhuanlan.zhihu.com/p/82244559)
38. [target_link_directories()1-CSDN博客](https://blog.csdn.net/qq_33726635/article/details/121896441)
39. [target_link_directories()2-CSDN博客](https://blog.csdn.net/zhizhengguan/article/details/115331314)
40. [add_definitions()-CSDN博客](https://blog.csdn.net/fb_941219/article/details/107376017)
41. [编译选项设置区别-CSDN博客](https://blog.csdn.net/10km/article/details/51731959)
42. [编译器警告-CSDN博客](https://blog.csdn.net/sexyluna/article/details/134770233)
43. [Options to Request or Suppress Warnings-GCC](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)
44. [CMake如何入门？-0xCCCCCCCC的回答-知乎](https://www.zhihu.com/question/58949190/answer/999701073)
45. [CMake和Modern CMake相关资料（不定期补充）-迦非喵的文章-知乎](https://zhuanlan.zhihu.com/p/205324774)
