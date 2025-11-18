---
layout: post
title: rosnode命令行工具学习笔记
date: 2023-03-06
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

我的rosnode命令行工具学习笔记。

<!-- more -->

## rosnode Hello World

1. `rosnode`命令行工具可以显示关于ROS节点（node）的调试信息，包括发布、订阅、连接信息等；
2. 语法说明：

    ```shell
    rosnode <subcommand> [options] [args]
    ```

3. 显示帮助信息：

    ```shell
    rosnode -h
    rosnode <subcommand> -h
    ```

## 子命令含义

| subcommand | 含义 |
| :--- | :--- |
| `info` | Print information about node. |
| `kill` | Kill a running node. |
| `list` | List active nodes. |
| `machine` | List nodes running on a particular machine or list machines. |
| `ping` | Test connectivity to node. |
| `cleanup` | Purge registration information of unreachable nodes. |

### `rosnode info`命令

#### 语法说明

```shell
rosnode info [options] node1 [node2...]
```

#### 选项含义

| options | 含义 |
| :--- | :--- |
| `-q`, `--quiet` | Prints only basic information such as pubs/subs and does not contact nodes for more information. |

### `rosnode kill`命令

#### 语法说明

```shell
rosnode kill [options] [node1 [node2...]]
```

1. 如果节点挂起，则可能无法被杀死；
2. 如果在`.launch`文件中将节点的`respawn`属性设置为`true`（默认为`false`），则节点在被杀死后可能重新出现：

    ```xml
    <node name="bar1" pkg="foo_pkg" type="bar" args="--test" respawn="true" />
    ```

3. 如果节点名缺省，则使用交互模式，常用于杀死匿名节点；

#### 选项含义

| options | 含义 |
| :--- | :--- |
| `-a`, `--all` | Kill all nodes. |

### `rosnode list`命令

#### 语法说明

```shell
rosnode list [options] [namespace]
```

`namespace`参数表示只显示指定命名空间`/namespace`中的节点名，例如`/namespace/***`；

#### 选项含义

| options | 含义 |
| :--- | :--- |
| `-u` | List XML-RPC URIs of current nodes. |
| `-a`, `--all` | List name and XML-RPC URIs (all info) of current nodes. |

### `rosnode machine`命令

#### 语法说明

```shell
rosnode machine [machine-name]
```

### `rosnode ping`命令

#### 语法说明

```shell
rosnode ping [options] node
```

#### 选项含义

| options | 含义 |
| :--- | :--- |
| `-a`, `--all` | Ping all nodes. |
| `-c COUNT` | Number of pings to send. Not available with `--all`. |

### `rosnode cleanup`命令

#### 语法说明

```shell
rosnode cleanup
```

## 参考

1. [rosnode-ROS Wiki](http://wiki.ros.org/rosnode)
2. [roslaunch/XML/node-ROS Wiki](http://wiki.ros.org/roslaunch/XML/node)
