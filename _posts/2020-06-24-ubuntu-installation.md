---
layout: post
title: Ubuntu安装记录及问题解决
date: 2020-06-24
author: zxl19
tags: [Ubuntu]
comments: true
toc: true
pinned: false
---

记录一下Ubuntu 16.04 LTS的安装过程及问题解决。

<!-- more -->

## 启动盘制作

1. 下载Ubuntu镜像文件；
2. 使用rufus制作启动盘;
3. 其余设置默认即可;
4. 选择以DD方式写入U盘中.

## 分区方案

1. 一种简单的方案是不分区，直接清除整个磁盘安装系统。
2. 采取硬盘分区方案，以下是一种分区方案：
    电脑配置：16GB内存、256GB固态硬盘、1T机械硬盘
    分区方案：将系统安装在固态硬盘中，将机械硬盘全部划分给`/home`

    | 名称 | 大小 | 逻辑or主分区 |
    | :----: | :----: | :----: |
    | EFI | 1024MB | 逻辑分区 |
    | swap |16384MB| 逻辑分区 |
    | / | 剩余固态硬盘 | 主分区 |
    | /home | 全部机械硬盘 | 逻辑分区 |

## 软件源设置

采用清华源，加快下载速度。

## 显卡驱动设置

采用NVIDIA提供的显卡驱动。

## 参考

1. [Get Ubuntu](https://ubuntu.com/download)
2. [Rufus](http://rufus.ie/)
3. [GitHub代下载服务](http://g.widyun.com/)
4. [Github镜像站](https://github.wuyanzheshui.workers.dev/)
5. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)
