---
layout: post
title: 在VS Code中搭建轻量C++开发环境
date: 2020-10-19
author: zxl19
tags: [C++, VS Code, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows系统中和Linux系统中的VS Code中搭建轻量化的C++开发环境。

<!-- more -->

## Windows

1. 下载安装VS Code，安装选项全部勾选；

    - 安装插件`Chinese (Simplified) Language Pack for Visual Studio Code`，`C/C++`；

2. 安装C++工具链`MinGW-w64`；

    - 包括编译器、调试器、链接器等；
    - 从[MinGW-64官网](http://mingw-w64.org/doku.php)上下载安装程序：`Downloads`->`MingW-W64-builds`->`Sourceforge`；
    - 右键`以管理员身份运行`；
    - 确定安装选项：

        | 内容 | 含义 | 选项 |
        | :------ | :------ | :------ |
        | Version | gcc版本，无具体要求选最新版本 | 8.1.0 |
        | Architecture | 操作系统架构 | 32位：i686；64位：x86_64 |
        | Threads | 接口协议 | Windows：win32；其它：posix |
        | Exception | 异常处理模型 | seh：新、性能好、不支持32位；sjlj：老、稳定性好，支持32位 |
        | Build revision | N/A | 默认 |

    - 设置安装目录，路径中不要有中文和空格，建议安装到C盘根目录下；
    - 自动下载安装；
    - 设置环境变量，将安装目录下的`bin`文件夹路径添加到环境变量中：右键`我的电脑`->`属性`->`高级系统设置`->`环境变量`->`系统变量`->`Path`->`编辑`->`新建`->粘贴`C:\mingw-w64\x86_64-8.1.0-win32-sjlj-rt_v6-rev0\mingw64\bin`；
    - 测试是否安装成功，在命令行中输入：

        ```shell
        gcc -v
        g++ -v
        gdb -v
        ```

        若能正确输出版本，则安装成功。

3. 编写代码，注意路径中不要有空格和中文，否则gdb可能无法正常工作；

    示例：

    ```cpp
    #include <iostream>
    #include <cstdlib>

    int main(int argc, char const *argv[])
    {
        std::cout << "Hello VSCode!" << std::endl;
        std::system("pause");
        return 0;
    }
    ```

4. 配置VS Code;

    - 点击左侧`运行`（`Ctrl`+`Shift`+`D`）->`创建launch.json文件`->`C++(GDB/LLDB)`->`g++.exe-生成和调试活动文件`，在当前目录`.vscode`文件夹中生成`launch.json`和`tasks.json`文件；
    - `launch.json`配置启动参数，调试器附加在可执行文件进程上进行debug，需要`preLaunchTask`先编译成可执行文件；
        - `externalConsole`是否启动外部控制台（黑色框框）；
        - `internalConsoleOptions`控制何时打开内部调试控制台，选择`neverOpen`，这样，内置窗口打开的是终端（terminal）而不是控制台（console），输入输出在内置终端上显示。
    - `tasks.json`配置任务参数，从源代码编译、链接生成可执行文件；
        - `Shift`+`Ctrl`+`P`打开命令控制台，选择`Tasks: Configure Task`配置任务，选择`C/C++: g++.exe build active file`创建`tasks.json`文件，可以在当中定义多个任务；
        - 作用：相当于在命令行中运行编译命令：

        ```shell
        g++ hello.cpp -o a.exe
        ```

        - `command`中使用的是绝对路径，由于已经添加环境变量，直接填`g++`也可；
        - `args`中为编译器参数，使用默认即可，高级功能详见编译器文档；
            - 使用C++语言标准：`"-std=c++17"`（注意参数间用逗号隔开）；
        - 如果使用纯C，`command`填`gcc`，`args`中语言标准用`-std=c11`；
    - `F5`编译运行调试；

5. 一个更复杂的例子；

    - 语法报错：插件设置默认C++98，新语法无法识别，在`设置`->`扩展`->`C++`中进行格式设置；
        - `Clang_format_sort includes`：是否对头文件排序；
        - `Cpp Standard`：C++20；
        - `C Standard`：C11；
    - 代码整理：`Shift`+`Alt`+`F`
        - `Clang_format_fallback Style`：全局设置格式标准，也可通过文件进行局部设置；
        - 可以基于某种标准进行修改；
    - `Shift`+`Ctrl`+`B`只编译`g++.exe build active file`，编译出`.exe`文件；
    - 添加断点调试，查看变量的值（不是所有容器都可以查看值）；

6. 多文件；

    - 使用Makefile；
    - 在`tasks.json`中修改`command`为`make`，`args`不再需要；
    - **使用CMake更加方便！自动生成Makefile。**

## Linux

1. 使用的发行版是Manjaro；
2. 安装VS Code，通过软件包管理器或者命令行；
3. Linux自带工具链，用上述方法查看版本进行检验，一般不需额外安装；
4. 打开工作区：

    ```shell
    code <path>
    ```

5. 安装插件，同上；
6. 编写代码；

    示例：

    ```cpp
    #include <iostream>
    #include <string>

    int main(int argc, char const *argv[])
    {
        std::string str;
        std::cin >> str;
        std::cout << "Echo: " << str << std::endl;
        return 0;
    }
    ```

7. 配置VS Code，步骤同上；

    - 注意：`launch.json`中的`preLaunchTask`应当与`tasks.json`中的`label`名称一致；
    - Linux中控制台默认保持，程序中不需暂停；

## 参考

1. [使用VS Code搭建轻量美观的C/C++开发环境-bilibili](https://www.bilibili.com/video/BV1sW411v7VZ)
2. [MinGW-64](http://mingw-w64.org/doku.php)
3. [MinGW-64安装-博客园](https://www.cnblogs.com/ggg-327931457/p/9694516.html)
4. [Using C++ on Linux in VS Code](https://code.visualstudio.com/docs/cpp/config-linux)
