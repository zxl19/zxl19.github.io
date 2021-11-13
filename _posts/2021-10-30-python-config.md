---
layout: post
title: Python读取配置文件
date: 2021-10-30
author: zxl19
tags: [Python, Note]
comments: true
toc: true
pinned: false
---

Python读取配置文件的方法，使用标准库中的`configparser`模块读取`.ini`格式的配置文件。

<!-- more -->

## 配置文件格式说明

1. `.ini`格式的配置文件由若干个节（section）组成，每个节中包含键（key）及其对应的值（value），节、键、值中可以包含空格；
2. 使用`[]`将节名括起来；
3. 键不区分大小写，以小写形式存储；
4. 值可以为空，在存储和读取时被当做字符串，非字符串类型的值需要进行类型转换，后续将进行详细说明；
5. 使用`=`分隔键和值，也可以使用`:`，分隔符左右可以添加空格；
6. 使用`;`添加注释，也可以使用`#`；
7. 名为`DEFAULT`的节为默认节，在使用`get()`函数时其中的默认值优先于回退值（fallback value），后续将进行详细说明；

配置文件示例：

```ini
[DEFAULT]
key1 = This is a string.
key2 = 100
key3 = 1.0
key4 = True

[SECTION_NAME]
; key1 = This is another string.
; key2 = 200
; key3 = 2.0
; key4 = False
```

## 配置文件创建

### 手动写入

如题，直接写入创建的`.ini`文件即可。

### 程序写入

语法类似于字典。

示例：

```python
import configparser

config = configparser.ConfigParser()
# 以下三种方法等价：
# 方法1
config['DEFAULT'] = {'key1': 'This is a string.',
                     'key2': '100',
                     'key3': '1.0',
                     'key4': 'True'}
# 方法2
config['DEFAULT'] = {}
config['DEFAULT']['key1'] = 'This is a string.'
config['DEFAULT']['key2'] = '100'
config['DEFAULT']['key3'] = '1.0'
config['DEFAULT']['key4'] = 'True'
# 方法3
config['DEFAULT'] = {}
default_config = config['DEFAULT']
default_config['key1'] = 'This is a string.'
default_config['key2'] = '100'
default_config['key3'] = '1.0'
default_config['key4'] = 'True'

with open('config.ini', 'w') as configfile:
    config.write(configfile)
```

## 配置文件读取

### 基础API

默认按照字符串读取并存储。

示例：

```python
import configparser

config = configparser.ConfigParser()
config.read('config.ini')
# 显示各节名称，不包括默认节
config.sections()
# 以下四种方法等价：
# 方法1
value1 = config['DEFAULT']['key1']
# 方法2
default_config = config['DEFAULT']
value1 = default_config['key1']
# 方法3
value1 = config.get('DEFAULT', 'key1')
# 方法4
value1 = config['DEFAULT'].get('key1')
```

### 数据类型转换

建议使用对应的成员函数进行类型转换，不推荐使用显式类型转换，因为`bool('False')=True`。

示例：

```python
# 字符串
value1 = config.get('DEFAULT', 'key1')
# 整型
value2 = config.getint('DEFAULT', 'key2')
value2 = int(config.get('DEFAULT', 'key2'))
# 浮点型
value3 = config.getfloat('DEFAULT', 'key3')
value3 = float(config.get('DEFAULT', 'key3'))
# 布尔型
value4 = config.getboolean('DEFAULT', 'key4')
```

### 回退值

在使用成员函数读取键对应的值时，可以使用`fallback`关键词指定在键不存在时返回的值，即回退值。

需要注意的是，**默认值优先于回退值，如果键在默认节中有定义，则使用默认节中的值，回退值不起作用：**

```python
# 默认节中不存在同名的键，使用回退值
value5 = config.get('SECTION_NAME', 'key5', fallback = 'fallback_value')
# 默认节中存在同名的键，使用默认值，回退值不起作用
value1 = config.get('SECTION_NAME', 'key1', fallback = 'fallback_value')
```

## 参考

1. [configparser-Python Documentation](https://docs.python.org/3/library/configparser.html)
2. [读取配置文件-Stack Overflow](https://stackoverflow.com/questions/19379120/how-to-read-a-config-file-using-python)
