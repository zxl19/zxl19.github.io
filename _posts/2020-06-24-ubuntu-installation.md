---
layout: post
title: Ubuntu系统安装记录及问题解决
date: 2020-06-24
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下Ubuntu 16.04 LTS系统的安装过程及问题解决。

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
2. `F12`->`USB Boot Disk`->`Install Ubuntu`

### 戴尔

1. `F12`->`BIOS Setup`->`Secure Boot`->`OFF`
2. `F12`->`BIOS Setup`->`System Configuration`->`SATA Operation`->`AHCI`
3. `F12`->`USB Boot Disk`->`Install Ubuntu`

## 安装

1. 安装时不联网、不下载更新，正常安装；
2. 清除整个磁盘安装系统，如果不要求分区可以直接使用；
3. 如果需要硬盘分区，重新安装系统并设置硬盘分区方案，以下是一种分区方案：

    电脑配置：16GB内存、256GB固态硬盘、1T机械硬盘。

    分区方案：将系统安装在固态硬盘中，将机械硬盘全部划分给`/home`：

    | 分区 | 大小 | 类型 | 位置 | 格式 |
    | :------ | :------ | :------ | :------ | :------ |
    | EFI | 1GB | 逻辑分区 | 空间起始位置 | EFI系统分区 |
    | swap | 16GB| 逻辑分区 | 空间起始位置 | 交换空间 |
    | / | 剩余固态硬盘 | 主分区 | 空间起始位置 | Ext4日志文件系统 |
    | /home | 全部机械硬盘 | 逻辑分区 | 空间起始位置 | Ext4日志文件系统 |

4. `/`目录在安装时默认格式化，勾选`/home`目录将其格式化，可以删除之前系统的配置文件；

## 安装后设置

### 软件源

采用清华源，加快下载速度。

### 显卡驱动

`系统设置`->`软件更新`->`附加驱动`

选择显卡厂商提供的驱动。

## 常见问题及解决方法

### 重新制作启动盘时U盘容量变小

1. `此电脑`->`管理`->`存储`->`磁盘管理`，确定U盘容量；
2. 在命令行中或者`Win`+`R`运行`diskpart`，打开分区工具；
3. 使用`list disk`命令列出磁盘列表，找到需要格式化的U盘及其对应编号：

    ```shell
      磁盘 ###  状态           大小     可用     Dyn  Gpt
      --------  -------------  -------  -------  ---  ---
      磁盘 0    联机              238 GB      0 B        *
      磁盘 1    联机              931 GB  1024 KB        *
      磁盘 2    联机               14 GB    14 GB
    ```

4. 使用`select disk = 2`选择需要格式化的U盘，重复运行`list disk`，可以看出，被选中的磁盘前出现`*`符号，表明其已被选中：

    ```shell
      磁盘 ###  状态           大小     可用     Dyn  Gpt
      --------  -------------  -------  -------  ---  ---
      磁盘 0    联机              238 GB      0 B        *
      磁盘 1    联机              931 GB  1024 KB        *
    * 磁盘 2    联机               14 GB    14 GB
    ```

5. 使用`clean`命令清除磁盘空间；
6. 在磁盘管理中选择对应磁盘，右键选择`新建简单卷`，新建分卷并格式化；

### 重装系统后旧系统配置文件未删除

在重装系统时勾选`/home`目录将其格式化，可以删除之前系统的配置文件。

下面的操作可以删除旧系统的配置文件，但是可能会同时删除`~/.bashrc`文件，导致命令行字体无颜色显示等一系列问题：

1. 使用`Ctrl`+`H`查看隐藏文件和文件夹；
2. 删除主目录下的隐藏文件和文件夹并重装系统；

### 重装系统后无`~/.bashrc`文件

1. 复制系统中的备份文件：

    ```shell
    cp  /etc/skel/.bashrc   ~/
    ```

2. 读取配置文件，使更改生效：

    ```shell
    source ~/.bashrc
    ```

### 无法联网

重启网络服务：

```shell
sudo service network-manager stop
sudo service network-manager start
```

或者：

```shell
sudo service network-manager restart
```

## 参考

1. [Ubuntu downloads](https://ubuntu.com/download)
2. [Alternative downloads](https://ubuntu.com/download/alternative-downloads)
3. [Rufus](https://rufus.ie/zh/)
4. [GitHub代下载服务](http://g.widyun.com/)
5. [GitHub镜像站](https://github.wuyanzheshui.workers.dev/)
6. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)
7. [如何解决U盘装系统后磁盘总容量变小？-百度经验](https://jingyan.baidu.com/article/59703552e754e48fc00740ed.html)
8. [重装Ubuntu时如何保留/home分区中的数据-博客园](https://www.cnblogs.com/maowang1991/p/3270441.html)
9. [Ubuntu下~/.bashrc文件的恢复方法-CSDN博客](https://blog.csdn.net/yucicheung/article/details/79334998)
10. [无法联网-CSDN博客](https://blog.csdn.net/nickdada/article/details/118152182)
11. [重启网络服务-Stack Exchange](https://askubuntu.com/questions/230698/how-to-restart-the-networking-service)
