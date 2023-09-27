---
layout: post
title: 在Ubuntu系统中查看依赖库信息
date: 2023-03-21
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中查看依赖库信息。

<!-- more -->

## 使用`ldconfig`命令

### 命令说明

1. `ldconfig`命令用于为共享库（shared library）依赖项配置符号链接（symbolic link）和缓存；
2. 默认搜索`/lib`和`/usr/lib`目录以及`/etc/ld.so.conf`配置文件中的目录；
3. 语法说明：

    ```shell
    ldconfig [-nNvXV] [-f conf] [-C cache] [-r root] directory...
    ldconfig -l [-v] library...
    ldconfig -p
    ```

### 常用语法

1. 更新符号链接并重新构建缓存（通常在新安装库时进行）：

    ```shell
    sudo ldconfig
    ```

2. 更新指定目录的符号链接：

    ```shell
    sudo ldconfig -n path/to/directory
    ```

3. 打印缓存中的库并检查指定的库是否存在：

    ```shell
    ldconfig -p | grep library_name
    ldconfig --print-cache | grep library_name
    ```

    常用于检查系统中是否安装指定的共享库。

## 使用`ldd`命令

### 命令说明

1. `ldd`命令用于显示二进制文件的共享库依赖项；
2. 对于不受信任的二进制文件不能使用`ldd`命令，需要使用`objdump`命令，将在后文中详述；
3. 对于不同系统架构的二进制文件不能使用`ldd`命令，需要使用`readelf`命令，将在后文中详述；
4. 语法说明：

    ```shell
    ldd [option]... file...
    ```

### 常用语法

1. 显示二进制文件的共享库依赖项：

    ```shell
    ldd path/to/binary
    ```

2. 显示关于依赖项的所有信息：

    ```shell
    ldd -v path/to/binary
    ldd --verbose path/to/binary
    ```

3. 显示未使用的直接依赖项：

    ```shell
    ldd -u path/to/binary
    ldd --unused path/to/binary
    ```

4. 报告丢失的数据对象并进行数据重定位：

    ```shell
    ldd -d path/to/binary
    ldd --data-relocs path/to/binary
    ```

5. 报告丢失的数据对象和函数，并对于两者进行重定位：

    ```shell
    ldd -r path/to/binary
    ldd --function-relocs path/to/binary
    ```

    常用于检查链接共享库时存在的未定义符号问题，可能有四种原因：

    - 未将依赖的共享库添加到`CMakeLists.txt`中或者依赖的共享库不存在；
    - 在生成依赖的共享库时未将`.cpp`文件添加到`CMakeLists.txt`中；
    - 静态数据成员未在类外初始化；
    - 在与C语言混合编程时没有添加`extern "C"`;

## 使用`objdump`命令

### 命令说明

1. `objdump`命令用于查看关于对象文件的信息；
2. 语法说明：

    ```shell
    objdump <option(s)> <file(s)>
    ```

### 常用语法

1. 显示文件头（file header）信息：

    ```shell
    objdump -f binary
    objdump --file-headers binary
    ```

2. 显示可执行部分的反汇编（disassembled）输出：

    ```shell
    objdump -d binary
    objdump --disassemble binary
    ```

3. 以Intel语法显示可执行部分的反汇编输出：

    ```shell
    objdump -M intel -d binary
    objdump --disassembler-options=intel --disassemble binary
    ```

4. 显示完整二进制文件所有部分的十六进制转储（hex dump）：

    ```shell
    objdump -s binary
    objdump --full-contents binary
    ```

5. 显示所有报头（header）的内容并查看共享库依赖项：

    ```shell
    objdump -x binary | grep NEEDED
    objdump --all-headers binary | grep NEEDED
    ```

    常用于查看共享库依赖项的名称。

## 使用`readelf`命令

### 命令说明

1. `readelf`命令用于显示ELF文件信息；
2. 语法说明：

    ```shell
    readelf <option(s)> <file(s)>
    ```

### 常用语法

1. 显示有关ELF文件的所有信息：

    ```shell
    readelf -a path/to/binary
    readelf --all path/to/binary
    ```

2. 显示ELF文件中存在的所有报头：

    ```shell
    readelf -e path/to/binary
    readelf --headers path/to/binary
    ```

3. 显示ELF文件的符号表部分中的条目：

    ```shell
    readelf -s path/to/binary
    readelf --syms path/to/binary
    readelf --symbols path/to/binary
    ```

4. 显示ELF文件的文件头中包含的信息：

    ```shell
    readelf -h path/to/binary
    readelf --file-header path/to/binary
    ```

5. 显示ELF文件的动态部分并查看共享库依赖项：

    ```shell
    readelf -d path/to/binary | grep NEEDED
    readelf --dynamic path/to/binary | grep NEEDED
    ```

    常用于查看不同系统架构下的共享库依赖项名称。

## 使用`c++filt`命令

### 命令说明

1. `c++filt`命令用于还原（demangle）C++和Java符号；
2. 语法说明：

    ```shell
    c++filt [options] [mangled names]
    ```

3. 常用于解析编译后的符号名，从而恢复编译前的函数名；

## 使用`nm`命令

### 命令说明

1. `nm`命令用于列出对象文件中的符号名称；
2. 语法说明：

    ```shell
    nm [option(s)] [file(s)]
    ```

3. 默认对象文件名为`a.out`；

### 常用语法

1. 列出文件中的全局函数和外部函数，前缀为`T`：

    ```shell
    nm -g path/to/file.o
    nm --extern-only path/to/file.o
    ```

2. 列出文件中的未定义符号：

    ```shell
    nm -u path/to/file.o
    nm --undefined-only path/to/file.o
    ```

3. 列出文件中的全部符号，包括调试符号：

    ```shell
    nm -a path/to/file.o
    nm --debug-syms path/to/file.o
    ```

4. 还原C++符号，使其可读：

    ```shell
    nm -C path/to/file.o
    nm --demangle path/to/file.o
    ```

5. 在每个符号前打印输入文件的名称并查看指定符号：

    ```shell
    nm -A path/to/file.o | grep symbol_name
    nm --print-file-name path/to/file.o | grep symbol_name
    ```

    常用于查看指定的符号是否被定义，未定义符号前缀为`U`。

## 使用`chrpath`命令

### 命令说明

1. `chrpath`命令用于查看和修改二进制文件的运行时路径（runtime path，rpath）和运行时搜索路径（run-time search path，runpath）信息；
2. 语法说明：

    ```shell
    chrpath [-v|-d|-c|-r <path>] <program> [<program> ...]
    ```

3. 可用于修改可执行文件的rpath信息，使其在依赖库发生变化的环境中运行，一般情况下不建议使用；

## 使用`patchelf`命令

### 命令说明

1. `patchelf`命令用于修改ELF文件信息；
2. 语法说明：

    ```shell
    patchelf [--set-interpreter FILENAME] [--page-size SIZE]
             [--print-interpreter] [--print-soname]
             [--set-soname SONAME] [--set-rpath RPATH] [--remove-rpath]
             [--shrink-rpath] [--print-rpath] [--force-rpath]
             [--add-needed LIBRARY] [--remove-needed LIBRARY] [--replace-needed LIBRARY NEW_LIBRARY]
             [--print-needed] [--no-default-lib] [--debug] [--version]
             FILENAME
    ```

3. 可用于修改可执行文件的rpath信息，使其在依赖库发生变化的环境中运行，一般情况下不建议使用；

## 参考

1. [undefined symbol问题的查找、定位与解决方法-CSDN博客](https://blog.csdn.net/buknow/article/details/96130049)
2. [Linux动态库undefined symbol原因定位与解决方法-博客园](https://www.cnblogs.com/zoule/p/15002536.html)
3. [未定义符号的链接问题通用解决方法-博客园](https://www.cnblogs.com/thammer/p/17187860.html)
4. [c++符号表解析-CSDN博客](https://blog.csdn.net/wdjjwb/article/details/86233389)
5. [ldconfig命令-五月的麦田](https://www.cnblogs.com/my-show-time/p/15250435.html)
6. [C/C++开发技巧：ldconfig，ldd，objdump，readelf，lsof动态库命令行工具-CSDN博客](https://blog.csdn.net/yjkhtddx/article/details/109133890)
7. [linux下nm，objdump和ldd三大工具使用-CSDN博客](https://blog.csdn.net/hsy12342611/article/details/129322929)
8. [C++的“坑”之一：undefined reference-CrackingOysters的文章-知乎](https://zhuanlan.zhihu.com/p/425155409)
9. [mangle和demangle-博客园](https://www.cnblogs.com/robinex/p/7892795.html)
10. [一文搞懂动态链接库的各种路径的意义与设置-卷儿的文章-知乎](https://zhuanlan.zhihu.com/p/450986377)
11. [NixOS/patchelf](https://github.com/NixOS/patchelf)
