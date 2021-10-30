---
layout: post
title: Python读取rosbag数据
date: 2021-10-30
author: zxl19
tags: [Python, ROS, Note]
comments: true
toc: true
pinned: false
---

使用Python读取rosbag数据。

<!-- more -->

## 获取rosbag摘要信息

### 方法1

```python
import subprocess
import yaml

bagfile = 'input.bag'
info_dict = yaml.load(subprocess.Popen(['rosbag', 'info', '--yaml', bagfile], stdout=subprocess.PIPE).communicate()[0])
duration = info_dict['duration']
start_time = info_dict['start']
```

### 方法2

```python
import yaml
from rosbag.bag import Bag

bagfile = 'input.bag'
info_dict = yaml.load(Bag(bagfile, 'r')._get_yaml_info())
duration = info_dict['duration']
start_time = info_dict['start']
```

## 获取rosbag消息信息

```python
import rosbag

bag = rosbag.Bag('test.bag')
for topic, msg, t in bag.read_messages(topics=['chatter', 'numbers']):
# for topic, msg, t in bag.read_messages(): # 也可，遍历所有话题
    print(msg)
bag.close()
```

## 参考

1. [rosbag/Cookbook](http://wiki.ros.org/rosbag/Cookbook)
2. [rosbag/Code API](http://wiki.ros.org/rosbag/Code%20API)
