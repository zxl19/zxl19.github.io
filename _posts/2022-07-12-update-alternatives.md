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

格式说明：

```shell
sudo update-alternatives --install <link> <name> <path> <priority>
```

## 选择版本

```shell
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```

## 参考

1. [Stack Exchange](https://askubuntu.com/questions/26498/how-to-choose-the-default-gcc-and-g-version)
2. [腾讯云](https://cloud.tencent.com/developer/article/1532283)
3. [Stack Exchange](https://askubuntu.com/questions/1140183/install-gcc-9-on-ubuntu-18-04)
