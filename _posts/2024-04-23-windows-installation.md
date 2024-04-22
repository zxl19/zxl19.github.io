---
layout: post
title: Windows系统安装记录及问题解决
date: 2023-04-23
author: zxl19
tags: [Windows, Note]
comments: true
toc: true
pinned: false
---

记录一下Windows 10系统的安装过程及问题解决。

<!-- more -->

## 下载Windows系统镜像文件

1. [官网](https://www.microsoft.com/zh-cn/software-download/windows10)
2. [MSDN，我告诉你](https://msdn.itellyou.cn)
3. [NEXT, ITELLYOU](https://next.itellyou.cn)

## 制作U盘启动盘

1. 使用[Rufus](https://rufus.ie/zh/)制作U盘启动盘；
2. `设备`选择准备制作为启动盘的U盘；
3. `引导类型选择`选择Windows系统镜像文件；
4. `镜像选项`默认`标准Windows安装`；
5. `分区类型`默认`GPT`；
6. `目标系统类型`默认`UEFI（非CSM）`；
7. `Windows用户体验`勾选`使用当前用户的区域设置`；

## BIOS设置

1. 台式机使用主板上的USB接口；
2. 开机后使用`Del`或`F2`进入BIOS；
3. 选择启动盘：

    - GPT分区使用UEFI引导；
    - MBR分区使用Legacy引导；

4. 开启XMP内存自动超频；
5. `F10`保存并重启；

## 安装

1. 安装时不联网；
2. 设置用户名和密码；
3. 使用系统工具进行硬盘分区；
4. 重启时拔出U盘启动盘；

## 参考

1. [【装机教程】超详细WIN10系统安装教程，官方ISO直装与PE两种方法教程-bilibili](https://www.bilibili.com/video/BV1DJ411D79y)
2. [U盘到底用什么格式好？FAT32、NTFS还是exFAT？-科技圈的文章-知乎](https://zhuanlan.zhihu.com/p/86116170)
3. [NTFS, FAT32和exFAT文件系统有什么区别？-W-Pwn的文章-知乎](https://zhuanlan.zhihu.com/p/32364955)
4. [MBR与GPT：你的新硬盘应该选择哪一个？-红头发蓝胖子的文章-知乎](https://zhuanlan.zhihu.com/p/559229466)
5. [分区表GPT和MBR有什么区别-迷你兔数据恢复的文章-知乎](https://zhuanlan.zhihu.com/p/114350934)
6. [微PE工具箱](https://www.wepe.com.cn)
