---
layout: post
title: 在Windows和Ubuntu系统中实现窗口平铺
date: 2023-03-20
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统中实现窗口平铺。

<!-- more -->

## Windows

在Windows中，使用微软开发的PowerToys工具箱中的FancyZones工具可以满足大部分需求：

1. 长按`Shift`并拖动窗口将当前窗口平铺到指定区域；
2. `Win`+方向键将当前窗口平铺到指定区域；
3. 平铺区域样式可以自定义；

## Ubuntu

在Ubuntu中，实现窗口平铺的方案较多，但是大部分的配置过程较为复杂。其中x-tile可以作为软件包直接安装并配置，较为简便，但是仍无法达到类似Windows的使用体验。

### x-tile

#### 安装

```shell
sudo add-apt-repository ppa:giuspen/ppa
sudo apt update
sudo apt install x-tile
```

#### 配置

1. 取消勾选`Exit After Tile`；
2. `Edit`->`Preferences`设置首选项：

    - `Language`选择语言；
    - 对于主显示器，预留出任务栏的宽度以保证最佳的窗口平铺效果:
        - 勾选`Override Monitor 1 Tiling Area`；
        - `Position`设置平铺区域位置（左上角坐标）；
        - `Size`设置平铺区域大小（宽度和高度）；
        - 在1920*1080的分辨率下，任务栏宽度约为65像素；

#### 使用

```shell
x-tile [option]
```

## 参考

1. [Tiling window manager-Wikipedia](https://en.wikipedia.org/wiki/Tiling_window_manager)
2. [microsoft/PowerToys](https://github.com/microsoft/PowerToys)
3. [13 Best Tiling Window Managers for Linux-Tecmint](https://www.tecmint.com/best-tiling-window-managers-for-linux/)
4. [20 Best tiling window managers for Linux as of 2023-Slant](https://www.slant.co/topics/1902/~best-tiling-window-managers-for-linux)
5. [Linux app for snapping windows into "Zones"](https://forums.overclockers.com.au/threads/linux-app-for-snapping-windows-into-zones.1290063/)
6. [x tile-giuspen](https://www.giuspen.com/x-tile/)
7. [giuspen/x-tile](https://github.com/giuspen/x-tile)
