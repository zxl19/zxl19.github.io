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

### 使用第三方库

1. [tqdm/tqdm](https://github.com/tqdm/tqdm)
2. [verigak/progress](https://github.com/verigak/progress)
3. [rsalmei/alive-progress](https://github.com/rsalmei/alive-progress)
4. [PySimpleGUI/PySimpleGUI](https://github.com/PySimpleGUI/PySimpleGUI)

## 参考

1. [创建文件夹-CSDN博客](https://blog.csdn.net/vip_lvkang/article/details/76906718)
2. [rosbag/Cookbook](http://wiki.ros.org/rosbag/Cookbook)
3. [进度条-腾讯云](https://cloud.tencent.com/developer/article/1661478)
