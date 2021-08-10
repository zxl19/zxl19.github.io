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

## 下载Ubuntu系统镜像文件

在[官网](https://ubuntu.com/download)下载Ubuntu系统镜像文件`ubuntu-16.04.6-desktop-amd64.iso`，更早版本可在[此处](https://ubuntu.com/download/alternative-downloads)找到。

## 制作U盘启动盘

1. 使用[Rufus](https://rufus.ie/zh/)制作U盘启动盘；
2. `设备`选择准备制作为启动盘的U盘；
3. `引导类型选择`选择Ubuntu系统镜像文件；
4. 其余选项采取默认设置；
5. 选择`以DD镜像模式写入`；

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

## 安装后设置

### 软件源

采用清华源，加快下载速度。

### 显卡驱动

`系统设置`->`软件更新`->`附加驱动`

选择显卡厂商提供的驱动。

## 常见问题及解决方法

### 重新制作启动盘时U盘容量变小

1. `此电脑`->`管理`->`存储`->`磁盘管理`确定U盘容量；
2. 在命令行中或者`Win`+`R`运行`diskpart`，打开分区工具；
3. 使用`list disk`命令列出磁盘列表，找到需要格式化的U盘及其对应编号；

```shell
  磁盘 ###  状态           大小     可用     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  磁盘 0    联机              238 GB      0 B        *
  磁盘 1    联机              931 GB  1024 KB        *
  磁盘 2    联机               14 GB    14 GB
```

4. 使用`select disk = 2`选择需要格式化的U盘，重复运行`list disk`，可以看出，被选中的磁盘前出现`*`符号，表明其已被选中；

```shell
  磁盘 ###  状态           大小     可用     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  磁盘 0    联机              238 GB      0 B        *
  磁盘 1    联机              931 GB  1024 KB        *
* 磁盘 2    联机               14 GB    14 GB
```

5. 使用`clean`命令清除磁盘空间；
6. 在磁盘管理中选择对应磁盘，右键选择`新建简单卷`，新建分卷并格式化；

## 参考

1. [Ubuntu downloads](https://ubuntu.com/download)
2. [Alternative downloads](https://ubuntu.com/download/alternative-downloads)
3. [Rufus](https://rufus.ie/zh/)
4. [GitHub代下载服务](http://g.widyun.com/)
5. [GitHub镜像站](https://github.wuyanzheshui.workers.dev/)
6. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)
7. [如何解决U盘装系统后磁盘总容量变小？-百度经验](https://jingyan.baidu.com/article/59703552e754e48fc00740ed.html)
