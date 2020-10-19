---
layout: post
title: 在VS Code中搭建轻量C++开发环境
date: 2020-10-19
author: zxl19
tags: [VS Code, C++]
comments: true
toc: true
pinned: false
---

记录如何在Windows系统下和Ubuntu系统下的VS Code中搭建轻量化的C++开发环境。

<!-- more -->

## Windows

1. 下载安装VS Code，安装选项全部勾选；
    + 安装插件`Chinese (Simplified) Language Pack for Visual Studio Code`，`C/C++`。
2. 安装C++工具链`MinGW-w64`；
    + 包括编译器、调试器、链接器等；
    + 从[MinGW-64官网](http://mingw-w64.org/doku.php)上下载安装程序：`Downloads`->`MingW-W64-builds`->`Sourceforge`；
    + 右键`以管理员身份运行`；
    + 确定安装选项：

        | 内容 | 含义 | 选项 |
        | :----: | :----: | :----: |
        | Version | gcc版本，无具体要求选最新版本 | 8.1.0 |
        | Architecture | 操作系统架构 | 32位：i686；64位：x86_64 |
        | Threads | 接口协议 | Windows：win32；其它：posix |
        | Exception | 异常处理模型 | seh：新、性能好、不支持32位；sjlj：老、稳定性好，支持32位 |
        | Build revision | N/A | 默认 |

    + 设置安装目录，路径中不要有中文和空格，建议安装到C盘根目录下；
    + 自动下载安装；
    + 设置环境变量，将安装目录下的`bin`文件夹路径添加到环境变量中：右键`我的电脑`->`属性`->`高级系统设置`->`环境变量`->`系统变量`->`Path`->`编辑`->`新建`->粘贴`C:\mingw-w64\x86_64-8.1.0-win32-sjlj-rt_v6-rev0\mingw64\bin`；
    + 测试是否安装成功，在命令行中输入：

        ```shell
        gcc -v
        g++ -v
        gdb -v
        ```

        若能正确输出版本，则安装成功。
3. 编写代码，注意路径中不要有空格和中文，否则gdb可能无法正常工作；

    ```C++
    #include <iostream>

    int main(int argc, char const *argv[])
    {
        std::cout << "Hello VSCode!" << std::endl;
        return 0;
    }
    ```

4. 配置VS Code;
    + 点击左侧`运行`（`Ctrl`+`Shift`+`D`）->`创建launch.json文件`->`C++(GDB/LLDB)`->`g++.exe-生成和调试活动文件`，在当前目录`.vscode`文件夹中生成`launch.json`和`tasks.json`文件

## Ubuntu

## 参考

1. [BV1sW411v7VZ](https://www.bilibili.com/video/BV1sW411v7VZ)
2. [MinGW-64](http://mingw-w64.org/doku.php)
3. [博客园](https://www.cnblogs.com/ggg-327931457/p/9694516.html)
