---
layout: post
title: ROS Kinetic安装记录及问题解决
date: 2020-06-24
author: zxl19
tags: [ROS, Note]
comments: true
toc: true
pinned: false
---

记录一下ROS Kinetic的安装过程及问题解决。

<!-- more -->

## 安装流程

全部流程参考官网的说明即可，采用清华源可以加速下载。

## sudo rosdep init失败的解决方式

在执行`sudo rosdep init`时报错：

```shell
ERROR: cannot download default sources list from:
https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list
Website may be down.
```

解决方案：

1. 直接跳过；

    不影响大部分情况下的使用，但是会影响后续一些ROS功能包的安装。

2. 电脑连接手机热点重试；

    可能无效。

3. 修改hosts文件；

    将`199.232.28.133 raw.githubusercontent.com`添加到自己电脑的hosts文件里面，文件路径为`/etc/hosts`。

4. 科学上网；

## 参考

1. [Ubuntu install of ROS Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu)
2. [sudo rosdep init失败-CSDN博客](https://blog.csdn.net/Bryantaoli/article/details/104730474/)
