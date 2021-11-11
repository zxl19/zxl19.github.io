---
layout: post
title: Ubuntu系统命令行使用代理
date: 2021-08-13
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

在安装代理工具后，在Ubuntu 18.04系统中使用`proxychains4`工具在命令行中使用代理。

<!-- more -->

## 系统配置

1. 操作系统：Ubuntu 18.04；
2. 代理工具已安装并正常运行；

## 安装

```shell
sudo apt update
sudo apt install proxychains4
```

## 配置

1. 打开配置文件：

    ```shell
    sudo gedit /etc/proxychains4.conf
    ```

2. 在配置文件最后进行设置：

    ```text
    # socks4 127.0.0.1 9050 # 注释掉原内容
    socks5 127.0.0.1 1080   # 代理使用的端口
    ```

## 使用

在需要使用代理的命令前添加`proxychains4`即可，如果Git已配置代理可不使用`proxychains4`。

示例：

```shell
sudo proxychains4 rosdep init
proxychains4 rosdep update
```

## 参考

1. [Ubuntu下实现命令行走代理/终端走代理的方法-lyh458的文章-知乎](https://zhuanlan.zhihu.com/p/377550825)
