---
layout: post
title: Ubuntu安装记录及问题解决
date: 2020-06-24
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下Ubuntu 16.04 LTS的安装过程及问题解决。

<!-- more -->

## 下载Ubuntu镜像文件

```shell
ubuntu-16.04.6-desktop-amd64.iso
```

## 制作安装U盘

1. 使用rufus制作;
2. 其余设置默认即可;
3. 选择以DD方式写入U盘中.

## 进入安全模式

### 联想

1. `F2`->`Security`->`Secure Boot`->`Disabled`
2. `F12`->`USB Disk`->`Install Ubuntu`

### 戴尔

1. `F12`->`BIOS Setup`->`Secure Boot`->`OFF`
2. `F12`->`BIOS Setup`->`System Configuration`->`SATA Operation`->`AHCI`
3. `F12`->`USB Disk`->`Install Ubuntu`

## 安装

1. 安装时不联网、不下载更新；
2. 清除整个磁盘安装系统，如果不要求分区可以直接使用；
3. 如果需要硬盘分区，重新安装系统并设置硬盘分区方案，以下是一种分区方案：

    电脑配置：16GB内存、256GB固态硬盘、1T机械硬盘

    分区方案：将系统安装在固态硬盘中，将机械硬盘全部划分给`/home`

    | 目录 | 大小 | 格式 | 类型 |
    | :------ | :------ | :------ | :------ |
    | EFI | 1GB | ext4 | 逻辑分区 |
    | swap | 16GB| swap | 逻辑分区 |
    | / | 剩余固态硬盘 | ext4 | 主分区 |
    | /home | 全部机械硬盘 | ext4 | 逻辑分区 |

## 软件源设置

采用清华源，加快下载速度。

## 显卡驱动设置

`系统设置`->`软件更新`->`附加驱动`

选择显卡厂商提供的驱动。

## 参考

1. [Get Ubuntu](https://ubuntu.com/download)
2. [Rufus](http://rufus.ie/)
3. [GitHub代下载服务](http://g.widyun.com/)
4. [GitHub镜像站](https://github.wuyanzheshui.workers.dev/)
5. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)
