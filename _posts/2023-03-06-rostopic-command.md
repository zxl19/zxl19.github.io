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

## rostpic Hello World

1. `rostopic`命令行工具可以显示关于ROS话题的信息，包括话题列表、发布订阅信息、频率、带宽、消息内容等；
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

1. 显示的带宽是接收带宽，受到网络连接状况的影响，接收带宽可能低于实际带宽；
2. `rostopic`命令行工具是基于Python实现的，无法达到与C++实现节点相似的吞吐量（throughput）；

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-w WINDOW_SIZE`, `--window WINDOW_SIZE` | Window size, in # of messages, for calculating rate. |

### `rostopic delay`命令

#### 语法说明

```shell
rostopic delay [options] topic
```

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

1. 可以使用`/topic/field`指定显示消息中的特定字段；

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

1. `namespace`参数表示只显示指定命名空间`/namespace`下的消息名，例如`/namespace/***`；

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

1. 指定消息字段的三种方法：

    ```shell
    # Command-line arguments. Defaults to latch mode.
    rostopic pub my_topic std_msgs/String "hello there"
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
