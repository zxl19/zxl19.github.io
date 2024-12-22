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
2. 代理工具已安装并正常运行，使用的IP地址和端口以`127.0.0.1:1080`为例：

    - 查看使用代理端口的进程：

        ```shell
        lsof -i:1080
        ```

    - 查看代理使用的公网IP：

        ```shell
        curl --socks5 127.0.0.1:1080 ip.sb      # 只显示IPv4
        curl --socks5 127.0.0.1:1080 cip.cc     # 显示IPv4和地址信息
        ```

    - 查看路由表：

        ```shell
        route -n
        ```

## 安装

```shell
sudo apt install proxychains4
```

## 配置

1. 打开`proxychains4`工具的默认配置文件：

    ```shell
    sudo gedit /etc/proxychains4.conf
    ```

2. 在配置文件最后进行设置：

    ```text
    # socks4 127.0.0.1 9050 # 注释掉原内容
    socks5 127.0.0.1 1080   # 代理使用的端口
    ```

## 使用

1. 在需要使用代理的命令前添加`proxychains4`即可：

    ```shell
    proxychains4 [ -f configfile.conf ] <program>
    ```

    示例：

    ```shell
    sudo proxychains4 rosdep init
    proxychains4 rosdep update
    ```

2. 如果Git已配置代理可不使用`proxychains4`；
3. 由于`proxychains4`只代理TCP连接，而`ping`命令使用ICMP连接，所以无法使用`proxychains4`代理`ping`命令；

## 参考

1. [Ubuntu下实现命令行走代理/终端走代理的方法-lyh458的文章-知乎](https://zhuanlan.zhihu.com/p/377550825)
2. [linux命令行代理神器-proxychains-TimeMachine的文章-知乎](https://zhuanlan.zhihu.com/p/166375631)
3. [什么是公网IP?公网IP与内网IP的区别？-埃文科技的文章-知乎](https://zhuanlan.zhihu.com/p/402559611)
4. [Linux查看公网IP和私网(内网)IP的方法-CSDN博客](https://blog.csdn.net/xiao_yi_xiao/article/details/120493210)
