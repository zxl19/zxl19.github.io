---
layout: post
title: rosbag相关命令行指令
date: 2021-06-08
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

rosbag相关的命令行指令。

<!-- more -->

## 基本格式

```shell
rosbag <subcommand>
```

## 命令详解

| subcommand | 含义 |
| :------ | :------|
| record | Record a bag file with the contents of specified topics. |
| info | Summarize the contents of a bag file. |
| play | Play back the contents of one or more bag files. |
| check | Determine whether a bag is playable in the current system, or if it can be migrated. |
| fix | Repair the messages in a bag file so that it can be played in the current system. |
| filter | Convert a bag file using Python expressions. |
| compress | Compress one or more bag files. |
| decompress | Decompress one or more bag files. |
| reindex | Reindex one or more broken bag files. |

## 参考

1. [rosbag/Commandline](http://wiki.ros.org/rosbag/Commandline)