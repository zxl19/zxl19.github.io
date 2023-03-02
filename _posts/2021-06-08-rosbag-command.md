---
layout: post
title: rosbag命令行工具学习笔记
date: 2021-06-08
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

我的rosbag命令行工具学习笔记。

<!-- more -->

## rosbag Hello World

1. rosbag是ROS中用于存储ROS消息数据的文件格式，文件名后缀为`.rosbag`；
2. 使用`rosbag`命令行工具可以对于rosbag中的数据进行记录、回放、操作；
3. 语法说明：

    ```shell
    rosbag <subcommand> [options] [args]
    ```

4. 显示帮助信息：

    ```shell
    rosbag -h
    rosbag <subcommand> -h
    ```

## 子命令含义

| subcommand | 含义 |
| :------ | :------|
| `record` | Record a bag file with the contents of specified topics. |
| `info` | Summarize the contents of a bag file. |
| `play` | Play back the contents of one or more bag files. |
| `check` | Determine whether a bag is playable in the current system, or if it can be migrated. |
| `fix` | Repair the messages in a bag file so that it can be played in the current system. |
| `filter` | Convert a bag file using Python expressions. |
| `compress` | Compress one or more bag files. |
| `decompress` | Decompress one or more bag files. |
| `reindex` | Reindex one or more broken bag files. |

### `rosbag record`命令

#### 语法说明

```shell
rosbag record TOPIC1 [TOPIC2 TOPIC3 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `-a`, `--all` | Record all topics. |
| `-e`, `--regex` | Match topics using regular expressions. |
| `-p`, `--publish` | Publish a message when the record begin to write a new bag (topic = "begin_write"). |
| `-x EXCLUDE_REGEX`, `--exclude=EXCLUDE=REGEX` | Exclude topics matching the given regular expression (subtracts from `-a` or `-e`). |
| `-q`, `--quiet` | Suppress console output. |
| `-d`, `--duration` | Specify the maximum duration of the recorded bag file. |
| `-o PREFIX`, `--output-prefix=PREFIX` | Prepend `PREFIX` to beginning of bag name before date stamp. |
| `-O NAME`, `--output-name=NAME` | Record to bag with name `NAME.bag`. |
| `--split` | Split the bag when maximum size (`--size`) or duration (`--duration`) is reached. |
| `--max-splits=MAX_SPLITS` | Split bag at most `MAX_SPLITS` times, then begin deleting the oldest files. This creates a fixed size or duration recording. |
| `-b SIZE`, `--buffsize=SIZE` | Use an internal buffer of `SIZE` MB (Default: 256, 0 = infinite). This is the message queue of the recorder object, before messages are being passed on to the bag. Lowering this value might result in messages being dropped before they reach the recording process. |
| `--chunksize=SIZE` | Advanced. Record to chunks of `SIZE` KB (Default: 768). This is a buffer within the bag file object. Lowering this value will result in more writes to disk. |
| `-l NUM`, `--limit=NUM` | Only record `NUM` messages on each topic. |
| `--node=NODE` | Record all topics subscribed to by a specific node. |
| `-j`, `--bz2` | Use BZ2 compression. See compress for details. |
| `--lz4` | Use LZ4 compression. See compress for details. |
| `--tcpnodelay` | Use the TCP_NODELAY transport hint when subscribing to topics. |
| `--udp` | Use the UDP transport hint when subscribing to topics. |

### `rosbag info`命令

#### 语法说明

```shell
rosbag info [options] BAGFILE1 [BAGFILE2 BAGFILE3 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `-y`, `--yaml` | Print information in YAML format. |
| `-k KEY`, `--key=KEY` | Print information only on the given field (requires `-y`). |

### `rosbag play`命令

#### 语法说明

```shell
rosbag play BAGFILE1 [BAGFILE2 BAGFILE3 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `-p PREFIX`, `--prefix=PREFIX` | Prefix all output topics. |
| `-q`, `--quiet` | Suppress console output. |
| `-i`, `--immediate` | Play back all messages without waiting. |
| `--pause` | Start in paused mode. |
| `--queue=SIZE` | Use an outgoing queue of size `SIZE` (defaults to 0. As of 1.3.3 defaults to 100). |
| `--clock` | Publish the clock time. |
| `--hz=HZ` | Publish clock time at frequency `HZ` Hz (default: 100). |
| `-d SEC`, `--delay=SEC` | Sleep `SEC` seconds after every advertise call (to allow subscribers to connect). |
| `-r FACTOR`, `--rate=FACTOR` | Multiply the publish rate by `FACTOR`. |
| `-s SEC`, `--start=SEC` | Start `SEC` seconds into the bags. |
| `-u SEC`, `--duration=SEC` | Play only `SEC` seconds from the bag files. |
| `--skip-empty=SEC` | Skip regions in the bag with no messages for more than `SEC` seconds. |
| `-l`, `--loop` | Loop playback. |
| `-k`, `--keep-alive` | Keep alive past end of bag (useful for publishing latched topics). |
| `--try-future-version` | Still try to open a bag file, even if the version number is not known to the player. |
| `--topics` | Specify which topics to play back. |
| `--pause-topics` | Topics to pause on during playback. |
| `--bags=BAGS` | Bags files to play back from. |
| `--wait-for-subscribers` | Wait for at least one subscriber on each topic before publishing. |
| `--rate-control-topic=RATE_CONTROL_TOPIC` | Watch the given topic, and if the last publish was more than `RATE_CONTROL_MAX_DELAY` ago, wait until the topic publishes again to continue playback. |
| `--rate-control-max-delay=RATE_CONTROL_MAX_DELAY` | Maximum time difference from `RATE_CONTROL_TOPIC` before pausing. |

### `rosbag check`命令

#### 语法说明

```shell
rosbag check BAG [-g RULEFILE] [EXTRARULES1 EXTRARULES2 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `-g RULEFILE`, `--genrules=RULEFILE` | Generate a bag migration rule file named `RULEFILE`. |
| `-a`, `--append` | Append to the end of an existing bag migration rule file after loading. |
| `-n`, `--noplugins` | Do not load rule files via plugins. |

### `rosbag fix`命令

#### 语法说明

```shell
rosbag fix INBAG OUTBAG [EXTRARULES1 EXTRARULES2 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `-n`, `--noplugins` | Do not load rule files via plugins. |

### `rosbag filter`命令

#### 语法说明

```shell
rosbag filter [options] INBAG OUTBAG EXPRESSION
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `--print=PRINT-EXPRESSION` | Evaluate and print a Python expression for verbose debugging. Uses same variables as filter expression. |

### `rosbag compress`命令

#### 语法说明

```shell
rosbag compress [options] BAGFILE1 [BAGFILE2 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `--output-dir=DIR` | Write to directory `DIR`. |
| `-f`, `--force` | Force overwriting of backup file it it exists. |
| `-q`, `--quiet` | Suppress noncritical messages. |
| `-j`, `--bz2` | Use BZ2 to compress data. |
| `--lz4` | Use LZ4 to compress data. |

### `rosbag decompress`命令

#### 语法说明

```shell
rosbag decompress [options] BAGFILE1 [BAGFILE2 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `--output-dir=DIR` | Write to directory `DIR`. |
| `-f`, `--force` | Force overwriting of backup file it it exists. |
| `-q`, `--quiet` | Suppress noncritical messages. |

### `rosbag reindex`命令

#### 语法说明

```shell
rosbag reindex [options] BAGFILE1 [BAGFILE2 ...]
```

#### 选项含义

| options | 含义 |
| :------ | :------|
| `-h`, `--help` | Show the usage and exit. |
| `--output-dir=DIR` | Write to directory `DIR`. |
| `-f`, `--force` | Force overwriting of backup file it it exists. |
| `-q`, `--quiet` | Suppress noncritical messages. |

## 参考

1. [rosbag/Commandline-ROS Wiki](http://wiki.ros.org/rosbag/Commandline)
