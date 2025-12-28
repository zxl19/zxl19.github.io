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
3. `Win`+`Shift`+`~`自定义平铺区域样式；

## Ubuntu

在Ubuntu中，实现窗口平铺的方案较多，但是大部分的配置过程较为复杂。

### gTile

gTile可以作为GNOME扩展直接安装，使用体验较好。

#### 安装

1. 安装本地支持组件`chrome-gnome-shell`：

    ```shell
    sudo apt install chrome-gnome-shell
    gnome-shell --version
    ```

2. 安装浏览器扩展`GNOME Shell integration`；
3. 在[GNOME Shell Extensions](https://extensions.gnome.org)网站上安装和管理gTile扩展；

#### 使用

| 功能 | 快捷键 |
| :--- | :--- |
| 打开界面 | `Super`+`Enter` |
| 将当前窗口缩放到**左下角** | `Super`+`Alt`+`1` |
| 将当前窗口缩放到**正下方** | `Super`+`Alt`+`2` |
| 将当前窗口缩放到**右下角** | `Super`+`Alt`+`3` |
| 将当前窗口缩放到**左侧** | `Super`+`Alt`+`4` |
| 将当前窗口缩放到**中央** | `Super`+`Alt`+`5` |
| 将当前窗口缩放到**右侧** | `Super`+`Alt`+`6` |
| 将当前窗口缩放到**左上角** | `Super`+`Alt`+`7` |
| 将当前窗口缩放到**正上方** | `Super`+`Alt`+`8` |
| 将当前窗口缩放到**右上角** | `Super`+`Alt`+`9` |

1. 缩放位置与数字小键盘上的键位对应；
2. 重复按缩放快捷键可以改变缩放大小；

### x-tile

x-tile可以作为软件包直接安装并配置，较为简便，但是仍无法达到类似Windows的使用体验。

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

1. 语法说明：

    ```shell
    x-tile [option]
    ```

2. 选项含义：

    | option | 含义 |
    | :--- | :--- |
    | 缺省 | 打开主界面 |
    | `w` | open the x-tile main window without using the panel |
    | `z` | undo the latest tiling operation |
    | `f` | tile all opened windows vertically |
    | `h` | tile all opened windows horizontally |
    | `u` | tile all opened windows triangle-up |
    | `d` | tile all opened windows triangle-down |
    | `l` | tile all opened windows triangle-left |
    | `r` | tile all opened windows triangle-right |
    | `q` | quad tile all opened windows |
    | `g = g 0 = g 0 0` | tile all opened windows in a grid with automatic rows and columns |
    | `g rows = g rows 0` | tile all opened windows in a grid with given rows and automatic columns |
    | `g 0 cols` | tile all opened windows in a grid with automatic rows and given columns |
    | `g rows cols` | tile all opened windows in a grid with given rows and columns |
    | `1` | custom tile 1 all opened windows |
    | `2` | custom tile 2 all opened windows |
    | `i` | invert the order of the latest tiling operation |
    | `y` | cycle the order of the latest tiling operation |
    | `m` | maximize all opened windows |
    | `M` | unmaximize all opened windows |
    | `c` | close all opened windows |

## 平铺式窗口管理器

1. 平铺式窗口管理器（Tiling Window Manager，TWM）：窗口之间不重叠，通过快捷键调整布局；
2. 堆叠式窗口管理器（Stacking Window Manager，SWM）：窗口之间可以重叠，通过鼠标调整布局；

### Windows

1. [LGUG2Z/komorebi](https://github.com/LGUG2Z/komorebi)
2. [glzr-io/glazewm](https://github.com/glzr-io/glazewm)
3. [fuhsjr00/bug.n](https://github.com/fuhsjr00/bug.n)
4. [workspacer/workspacer](https://github.com/workspacer/workspacer)

### Linux

1. [hyprwm/Hyprland](https://github.com/hyprwm/Hyprland)
2. [swaywm/sway](https://github.com/swaywm/sway)
3. [i3/i3](https://github.com/i3/i3)
4. [baskerville/bspwm](https://github.com/baskerville/bspwm)
5. [awesomeWM/awesome](https://github.com/awesomeWM/awesome)
6. [qtile/qtile](https://github.com/qtile/qtile)
7. [leftwm/leftwm](https://github.com/leftwm/leftwm)
8. [Kintaro/wtftw](https://github.com/Kintaro/wtftw)
9. [hyprwm/Hypr](https://github.com/hyprwm/Hypr)

### macOS

1. [asmvik/yabai](https://github.com/asmvik/yabai)
2. [nikitabobko/AeroSpace](https://github.com/nikitabobko/AeroSpace)
3. [ianyh/Amethyst](https://github.com/ianyh/Amethyst)
4. [acsandmann/rift](https://github.com/acsandmann/rift)

## 参考

1. [Tiling window manager-Wikipedia](https://en.wikipedia.org/wiki/Tiling_window_manager)
2. [microsoft/PowerToys](https://github.com/microsoft/PowerToys)
3. [13 Best Tiling Window Managers for Linux-Tecmint](https://www.tecmint.com/best-tiling-window-managers-for-linux/)
4. [20 Best tiling window managers for Linux as of 2023-Slant](https://www.slant.co/topics/1902/~best-tiling-window-managers-for-linux)
5. [Linux app for snapping windows into "Zones"](https://forums.overclockers.com.au/threads/linux-app-for-snapping-windows-into-zones.1290063/)
6. [gTile-GNOME Shell Extensions](https://extensions.gnome.org/extension/28/gtile/)
7. [gTile/gTile](https://github.com/gTile/gTile)
8. [如何安装GNOME插件-techmoe的文章-知乎](https://zhuanlan.zhihu.com/p/36265103)
9. [x tile-giuspen](https://www.giuspen.com/x-tile/)
10. [giuspen/x-tile](https://github.com/giuspen/x-tile)
11. [Linux平铺窗口管理器（Tiling Window Manager）完全指南：从入门到精通-极客技术博客](https://geek-blogs.com/blog/linux-tiling-wm/)
12. [最佳Linux窗口管理器详解：从选择到配置的完全指南-极客技术博客](https://geek-blogs.com/blog/best-linux-window-manager/)
13. [i3窗口管理器终极定制指南丨Linux中国-Linux中国的文章-知乎](https://zhuanlan.zhihu.com/p/640577283)
14. [为什么我喜欢用bspwm来做我的Linux窗口管理器丨Linux中国-Linux中国的文章-知乎](https://zhuanlan.zhihu.com/p/365764430)
15. [如何配置linux平铺式窗口管理器i3wm？-新鲜水墨的回答-知乎](https://www.zhihu.com/question/62251457/answer/3082755339)
16. [如何配置linux平铺式窗口管理器i3wm？-李狗蛋LGD的回答-知乎](https://www.zhihu.com/question/62251457/answer/766512992)
17. [ArchLinux从零构建易用美观的i3wm+i3bar+rofi+nitrogen桌面环境（一）-Jeek的文章-知乎](https://zhuanlan.zhihu.com/p/23010659665)
18. [ArchLinux从零构建易用美观的i3wm+i3bar+rofi+nitrogen桌面环境（二）-Jeek的文章-知乎](https://zhuanlan.zhihu.com/p/23356434216)
