---
layout: post
title: 在Ubuntu系统中链接文件和目录
date: 2024-04-28
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中链接文件和目录。

<!-- more -->

## 使用`ln`命令

### 命令说明

1. `ln`命令用于创建指向文件和目录的链接；
2. 链接分为硬链接（hard link）和符号链接（symbolic link），符号链接也被称为软链接；
3. 硬链接：

    - 硬链接和源文件指向同一索引节点（inode，index node），允许同一文件拥有多个有效路径；
    - 只有删除源文件和所有硬链接之后才会彻底删除数据，防止误删重要文件；
    - 不能跨文件系统，不能链接目录；

4. 符号链接：

    - 符号链接和源文件指向不同索引节点，符号链接包含源文件的路径信息，类似于Windows系统中的快捷方式；
    - 删除源文件或目录会导致符号链接失效，删除符号链接不影响源文件或目录；

5. 语法说明：

    ```shell
    ln [OPTION]... [-T] TARGET LINK_NAME   (1st form)
    ln [OPTION]... TARGET                  (2nd form)
    ln [OPTION]... TARGET... DIRECTORY     (3rd form)
    ln [OPTION]... -t DIRECTORY TARGET...  (4th form)
    ```

### 常用语法

1. 创建指向文件或目录的符号链接，要求目标符号链接不存在：

    ```shell
    ln -s path/to/file_or_directory path/to/symlink
    ```

2. 覆盖已有的符号链接，将其指向其他文件：

    ```shell
    ln -sf path/to/new_file path/to/symlink
    ```

3. 创建指向文件的硬链接：

    ```shell
    ln path/to/file path/to/hardlink
    ```

## 使用`update-alternatives`命令

### 命令说明

1. `update-alternatives`命令用于维护命令默认的符号链接；
2. 常用于管理不同版本的软件，通过符号链接指定默认使用的版本；
3. 语法说明：

    ```shell
    update-alternatives [<option> ...] <command>
    ```

### 常用语法

1. 添加符号链接：

    ```shell
    sudo update-alternatives --install path/to/symlink command_name path/to/command_binary priority
    ```

2. 配置符号链接：

    ```shell
    sudo update-alternatives --config command_name
    ```

3. 删除符号链接：

    ```shell
    # 删除指定命令的单个符号链接
    sudo update-alternatives --remove command_name path/to/command_binary
    # 删除指定命令的所有符号链接
    sudo update-alternatives --remove-all command_name
    ```

4. 显示指定命令的符号链接：

    ```shell
    update-alternatives --display command_name
    ```

5. 显示所有命令的符号链接：

    ```shell
    update-alternatives --get-selections
    ```

6. 按照优先级自动选择指定命令的符号链接：

    ```shell
    sudo update-alternatives --auto command_name
    ```

## 使用`readlink`命令

### 命令说明

1. `readlink`命令用于查看符号链接信息；
2. 语法说明：

    ```shell
    readlink [OPTION]... FILE...
    ```

### 常用语法

1. 查看符号链接指向的文件：

    ```shell
    readlink path/to/file
    ```

2. 递归查看符号链接指向的文件，要求除了最后一个组件外其余组件必须存在：

    ```shell
    readlink -f path/to/file
    readlink --canonicalize path/to/file
    ```

3. 递归查看符号链接指向的文件，要求所有组件必须存在：

    ```shell
    readlink -e path/to/file
    readlink --canonicalize-existing path/to/file
    ```

4. 递归查看符号链接指向的文件，不要求组件存在：

    ```shell
    readlink -m path/to/file
    readlink --canonicalize-missing path/to/file
    ```

## 参考

1. [Linux软连接和硬链接-Heropoo的文章-知乎](https://zhuanlan.zhihu.com/p/67366919)
2. [硬链接和符号链接详解-CSDN博客](https://blog.csdn.net/qq_41816540/article/details/81556768)
