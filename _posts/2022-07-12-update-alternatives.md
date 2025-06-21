---
layout: post
title: 使用update-alternatives工具管理C++编译器和Python解释器版本
date: 2022-07-12
author: zxl19
tags: [C++, Python, Note]
comments: true
toc: true
pinned: false
---

使用update-alternatives工具管理C++编译器和Python解释器版本。

<!-- more -->

## 安装新版本

### C++编译器

以`gcc-9`和`g++-9`为例：

```shell
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install gcc-9 g++-9
```

### Python解释器

以`python3.7`为例：

```shell
sudo apt update
sudo apt install python3.7
```

## 删除版本列表

### C++编译器

```shell
sudo update-alternatives --remove-all gcc
sudo update-alternatives --remove-all g++
```

### Python解释器

```shell
sudo update-alternatives --remove-all python3
```

## 添加版本列表

### C++编译器

```shell
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 11
```

### Python解释器

```shell
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 6
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 7
```

## 选择版本

### C++编译器

```shell
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

### Python解释器

```shell
sudo update-alternatives --config python3
```

## 参考

1. [install gcc-9 on Ubuntu 18.04?-Stack Exchange](https://askubuntu.com/questions/1140183/install-gcc-9-on-ubuntu-18-04)
2. [How to choose the default gcc and g++ version?-Stack Exchange](https://askubuntu.com/questions/26498/how-to-choose-the-default-gcc-and-g-version)
3. [update-alternatives——linux软件版本管理命令-腾讯云](https://cloud.tencent.com/developer/article/1532283)
4. [ubuntu18.04安装python3.7-CSDN博客](https://blog.csdn.net/JohnJim0/article/details/108226362)
