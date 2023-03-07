---
layout: post
title: rostopic命令行工具学习笔记
date: 2023-03-06
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

我的rostopic命令行工具学习笔记。

<!-- more -->

## rostopic Hello World

1. `rostopic`命令行工具可以显示关于ROS话题（topic）的信息，包括话题列表、发布者（publisher）、订阅者（subscriber）、频率、带宽、消息（message）内容等；
2. 语法说明：

    ```shell
    rostopic <subcommand> [options] [args]
    ```

3. 显示帮助信息：

    ```shell
    rostopic -h
    rostopic <subcommand> -h
    ```

## 子命令含义

| subcommand | 含义 |
| :------ | :------|
| `bw` | Display bandwidth used by topic. |
| `delay` | Display delay for topic which has header. |
| `echo` | Print messages to screen. |
| `find` | Find topics by type. |
| `hz` | Display publishing rate of topic. |
| `info` | Print information about active topic. |
| `list` | Print information about active topics. |
| `pub` | Publish data to topic. |
| `type` | Print topic type. |

### `rostopic bw`命令

#### 语法说明

```shell
rostopic bw [options] topic
```

1. 显示的带宽是接收带宽，如果网络连接状况不佳，或者`rostopic`命令行工具无法跟上发布者，接收带宽可能低于真实带宽；
2. `rostopic`命令行工具是基于Python实现的，无法像基于C++实现的ROS节点一样保持高吞吐量（throughput）；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-w WINDOW_SIZE`, `--window WINDOW_SIZE` | Window size, in # of messages, for calculating rate. |

### `rostopic delay`命令

#### 语法说明

```shell
rostopic delay [options] topic
```

要求话题中的消息类型包含报头（header）；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-w WINDOW_SIZE`, `--window WINDOW_SIZE` | Window size, in # of messages, for calculating rate. |
| `--tcpnodelay` | Use the TCP_NODELAY transport hint when subscribing to topics. |

### `rostopic echo`命令

#### 语法说明

```shell
rostopic echo [options] topic
```

可以使用`/topic/field`指定显示话题中的消息字段（field）；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `--offset` | Display time in messages as offset from current time (e.g. to calculate lag/latency). |
| `--filter` | Display messages that match a specified Python expression. The Python expression can use any Python builtins plus the variable `m` (the message). |
| `-c` | Clear the screen after each message is published. Cannot be used with `-p`. |
| `-b` | Display messages in a bag file. |
| `-p` | Display messages in a matlab/octave-friendly plotting format. Cannot be used with `-c`. |
| `-w NUM_WIDTH` | Print all numeric values with a fixed width. |
| `--nostr`, `-noarr` | Exclude string and array fields from the plotting output. |
| `-n COUNT` | Echo `COUNT` messages and exit. |

### `rostopic find`命令

#### 语法说明

```shell
rostopic find msg-type
```

### `rostopic hz`命令

#### 语法说明

```shell
rostopic hz [options] topic1 [topic2 ...]
```

1. 显示的是消息的发布频率；
2. 默认显示命令运行时间内的平均频率；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-w WINDOW_SIZE` | Report rate using a window size (number of samples) for a temporally local estimate of the rate. |
| `--filter FILTER_EXPR` | Only report rate for messages that match the Python `FILTER_EXPR`. WARNING: this option has a large performance hit and shouldn't be used for high-rate topics. |

### `rostopic info`命令

#### 语法说明

```shell
rostopic info topic
```

### `rostopic list`命令

#### 语法说明

```shell
rostopic list [options] [namespace]
```

`namespace`参数表示只显示指定命名空间`/namespace`中的话题名，例如`/namespace/***`；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-b` | List topics in a bag file. |
| `-p` | List only publishers. |
| `-s` | List only subscribers. |
| `-v` | Verbose mode. |
| `--host` | Group list by hostname. |

### `rostopic pub`命令

#### 语法说明

```shell
rostopic pub topic type [data ...]
```

可以使用以下三种方法指定话题中发布的消息字段：

```shell
# Command-line arguments. Defaults to latch mode.
rostopic pub my_topic std_msgs/String "hello there"
rostopic pub -r 10 /cmd_vel geometry_msgs/Twist \
    '{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}'
# Piped input. Defaults to rate mode (10hz). Example usage:
rostopic echo chatter | rostopic pub bar std_msgs/String
# YAML data file. Defaults to rate mode (10hz). Example usage:
rostopic echo chatter > chatter.bagy    # Collect messages, then Ctrl-C
rostopic pub -f chatter.bagy bar std_msgs/String
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-l`, `--latch` | Enable latch mode. Latching mode is the default when using command-line arguments. |
| `-r RATE` | Enable rate mode. Rate mode is the default (10hz) when using piped or file input. |
| `-1`, `--once` | Enable once mode. |
| `-f FILE` | Read message fields from YAML file. YAML syntax is equivalent to output of `rostopic echo`. Messages are separated using YAML document separator `---`. To use only the first message in a file, use the `--latch` option. |

### `rostopic type`命令

#### 语法说明

```shell
rostopic type topic
```

## 参考

1. [rostopic-ROS Wiki](http://wiki.ros.org/rostopic)
