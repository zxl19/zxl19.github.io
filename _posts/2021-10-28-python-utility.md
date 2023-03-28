---
layout: post
title: 程序常用功能Python实现
date: 2021-10-28
author: zxl19
tags: [Python, Note]
comments: true
toc: true
pinned: false
---

一些程序常用功能的Python实现。

<!-- more -->

## 创建文件夹

```python
import os

def mkdir(path):
    folder = os.path.exists(path)
    if not folder:
        os.makedirs(path)
        print("Folder %s Created!" % (path))
    else:
        print("Folder %s Exists!" % (path))
```

## 复制文件

```python
import os
import shutil

file_list = os.listdir(src_path)
file_list.sort()
for file in file_list:
    src = os.path.join(src_path, file)
    dst = os.path.join(dst_path, file)
    shutil.copy(src, dst)
```

## 进度条

### 使用标准库

```python
import sys

def status(length, percent):
    sys.stdout.write('\x1B[2K') # Erase entire current line
    sys.stdout.write('\x1B[0E') # Move to the beginning of the current line
    progress = "Progress: ["
    for i in range(0, length):
        if i < length * percent:
            progress += '='
        else:
            progress += ' '
    progress += "] " + str(round(percent * 100.0, 2)) + "%"
    sys.stdout.write(progress)
    sys.stdout.flush()
```

### 使用tqdm库

```python
from tqdm import tqdm

for i in tqdm(range(10000)):
    ...
```

## 参考

1. [创建文件夹-CSDN博客](https://blog.csdn.net/vip_lvkang/article/details/76906718)
2. [用Python复制文件的9个方法-景略集智的文章-知乎](https://zhuanlan.zhihu.com/p/35725217)
3. [python之shutil模块11个常用函数详解-CDA数据分析师的文章-知乎](https://zhuanlan.zhihu.com/p/213919757)
4. [rosbag/Cookbook-ROS Wiki](http://wiki.ros.org/rosbag/Cookbook)
5. [进度条-腾讯云](https://cloud.tencent.com/developer/article/1661478)
