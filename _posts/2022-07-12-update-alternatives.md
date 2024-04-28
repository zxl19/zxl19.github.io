---
layout: post
title: 使用update-alternatives工具管理C++编译器版本
date: 2022-07-12
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

使用update-alternatives工具管理C++编译器版本。

<!-- more -->

## 安装新版本C++编译器

以`gcc-9`和`g++-9`为例：

```shell
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install gcc-9 g++-9
```

## 删除版本列表

```shell
sudo update-alternatives --remove-all gcc
sudo update-alternatives --remove-all g++
```

## 添加版本列表

```shell
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 11
```

## 选择版本

```shell
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

## 参考

1. [install gcc-9 on Ubuntu 18.04?-Stack Exchange](https://askubuntu.com/questions/1140183/install-gcc-9-on-ubuntu-18-04)
2. [How to choose the default gcc and g++ version?-Stack Exchange](https://askubuntu.com/questions/26498/how-to-choose-the-default-gcc-and-g-version)
3. [update-alternatives——linux软件版本管理命令-腾讯云](https://cloud.tencent.com/developer/article/1532283)
