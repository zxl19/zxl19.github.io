---
layout: post
title: 在Ubuntu系统中切换并卸载系统内核
date: 2022-09-20
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中切换并卸载系统内核。

<!-- more -->

## 切换系统内核

1. 查看当前使用的系统内核：

    ```shell
    uname -a
    ```

2. 查看已安装的系统内核版本：

    ```shell
    sudo dpkg --get-selections | grep linux-image
    ```

    结果示例：

    ```shell
    linux-image-5.4.0-125-generic           install
    linux-image-5.0.0-23-generic            hold
    linux-image-5.4.0-64-generic            hold
    ```

3. 重启电脑，在启动时选择所需版本的系统内核，以`5.4.0-64-generic`为例：

    `Esc`->`Advanced options for Ubuntu`->`Ubuntu, with Linux 5.4.0-64-generic`；

## 卸载系统内核

1. 查看与需要卸载版本的系统内核相关的安装包，以`5.4.0-64-generic`为例：

    ```shell
    sudo dpkg --get-selections | grep 5.4.0-125
    ```

    结果示例：

    ```shell
    linux-headers-5.4.0-125-generic         install
    linux-hwe-5.4-headers-5.4.0-125         install
    linux-image-5.4.0-125-generic           install
    linux-modules-5.4.0-125-generic         install
    linux-modules-extra-5.4.0-125-generic   install
    ```

2. 卸载上述与需要卸载版本的系统内核相关的安装包：

    ```shell
    sudo apt purge <package>
    sudo apt purge
    sudo apt autoremove
    ```

3. 配置GRUB（可选）：

    - 查看配置文件：

        ```shell
        cat /etc/default/grub
        ```

    - 修改配置文件：

        ```text
        GRUB_DEFAULT=0              # 默认菜单项，默认值为0
        GRUB_TIMEOUT_STYLE=hidden   # 倒计时显示风格，默认值为menu，可选countdown、hidden
        GRUB_TIMEOUT=10             # 倒计时显示时间，默认值为5
        ```

4. 更新GRUB：

    ```shell
    sudo update-grub
    ```

## 安装系统内核

**如果没有特殊需求，不要手动安装或更新系统内核，可能会导致某些依赖于系统内核版本的软件无法正常运行。**

## 参考

1. [Ubuntu18.04安装及卸载内核-CSDN博客](https://blog.csdn.net/weixin_48395629/article/details/116055423)
2. [GRUB2配置文件详解-博客园](https://www.cnblogs.com/fluidog/p/15176726.html)
3. [Linux GRUB2配置简介-Linux中国](https://linux.net.cn/article-8603-1.html)
