---
layout: post
title: rosparam命令行工具学习笔记
date: 2026-08-16
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

我的`rosparam`命令行工具学习笔记。

<!-- more -->

## rosparam Hello World

1. `rosparam`命令行工具可以使用YAML编码的文件在参数服务器上获取和设置ROS参数；
2. 语法说明：

    ```shell
    rosparam <subcommand> [options] [args]
    ```

3. 显示帮助信息：

    ```shell
    rosparam -h
    rosparam <subcommand> -h
    ```

## YAML格式示例

1. 基本数据类型：

    ```yaml
    string: 'foo'
    integer: 1234
    float: 1234.5
    boolean: true
    list: [1.0, mixed list]
    dictionary: {a: b, c: d}
    ```

    - 在使用`rosparam`命令行工具设置字典类型参数时，字典会被解包为多个独立参数，**追加**到参数命名空间中，参数命名空间中的原有参数不变；
    - 在C++或Python节点中设置字典类型参数时，字典整体会被作为一个参数的值，**覆盖**到参数命名空间中，参数命名空间中的原有参数被覆盖；

2. 支持角度单位转换，任何Python合法的数学表达式都可以和弧度值一起使用，使用`pi`表示$\pi$：

    ```yaml
    angle1: rad(2*pi)
    angle2: deg(180)
    ```

    ```yaml
    angle1: !degrees 181.0
    angle2: !radians 3.14169
    ```

    都会转换为float类型的弧度值。

## 子命令含义

| subcommand | 含义 |
| :--- | :--- |
| `set` | Set parameter. |
| `get` | Get parameter. |
| `load` | Load parameters from file. |
| `dump` | Dump parameters to file. |
| `delete` | Delete parameter. |
| `list` | List parameter names. |

### `rosparam set`命令

#### 语法说明

```shell
rosparam set [options] parameter value
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-v` | Show verbose output. |
| `-t <text_file>, --textfile <text_file>` | Set parameter to contents of text file. |
| `-b <binary_file>, --binfile <binary_file>` | Set parameter to contents of binary file. Parameter Server will store value as an XML-RPC Binary type (Base 64 encoded). |

### `rosparam get`命令

#### 语法说明

```shell
rosparam get [options] parameter
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-p` | Pretty-print output. WARNING: this is not YAML-safe. |
| `-v` | Show verbose output. |

### `rosparam load`命令

#### 语法说明

```shell
rosparam load [options] file [namespace]
```

`namespace`参数表示只加载指定命名空间`/namespace`中的参数，例如`/namespace/***`，默认为`/`；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-v` | Show verbose output. |

### `rosparam dump`命令

#### 语法说明

```shell
rosparam dump [options] file [namespace]
```

`namespace`参数表示只保存指定命名空间`/namespace`中的参数，例如`/namespace/***`，默认为`/`；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-v` | Verbose output. |

### `rosparam delete`命令

#### 语法说明

```shell
rosparam delete [options] parameter
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-v` | Show verbose output. |

### `rosparam list`命令

#### 语法说明

```shell
rosparam list [namespace]
```

## 参考

1. [rosparam-ROS Wiki](https://wiki.ros.org/rosparam)
2. [Parameter Server-ROS Wiki](https://wiki.ros.org/Parameter%20Server)
3. [ROS/YAMLCommandLine-ROS Wiki](https://wiki.ros.org/ROS/YAMLCommandLine)
4. [roslaunch/XML/rosparam-ROS Wiki](https://wiki.ros.org/roslaunch/XML/rosparam)
5. [roslaunch/XML/param-ROS Wiki](https://wiki.ros.org/roslaunch/XML/param)
