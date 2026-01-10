---
layout: post
title: Ubuntu系统截图、录屏方法
date: 2021-11-07
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中截图和录屏，包括使用系统快捷键和第三方应用。

<!-- more -->

## 使用系统快捷键

### 截图

| 功能 | 快捷键 |
| :---- | :---- |
| 对于桌面截图 | `PrtSc` |
| 对于窗口截图 | `Alt`+`PrtSc` |
| 对于选定区域截图 | `Shift`+`PrtSc` |

### 录屏

使用`Ctrl`+`Alt`+`Shift`+`R`开始和结束录制，默认保存在`Videos`文件夹中。

## 使用Flameshot

支持截图并编辑。

### 安装

```shell
sudo apt install flameshot
```

## 使用Kazam

支持截图和录屏。

### 安装

```shell
sudo apt install kazam
```

### 设置

1. `Screencast`->`Framerate`->`25`；
2. `Screencast`->`Record with`->`H264(MP4)`；

## 使用Peek

支持录屏，已停止维护。

### 安装

```shell
sudo add-apt-repository ppa:peek-developers/stable
sudo apt update
sudo apt install peek
```

## GitHub

1. [flameshot-org/flameshot](https://github.com/flameshot-org/flameshot)
2. [phw/peek](https://github.com/phw/peek)
3. [GNOME/gimp](https://github.com/GNOME/gimp)
4. [shutter-project/shutter](https://github.com/shutter-project/shutter)
5. [hzbd/kazam](https://github.com/hzbd/kazam)
6. [KDE/spectacle](https://github.com/KDE/spectacle)

## 参考

1. [Screenshots and screencasts-Ubuntu Documentation](https://help.ubuntu.com/stable/ubuntu-help/screen-shot-record.html)
2. [在Linux下截屏并编辑的最佳工具-Linux中国的文章-知乎](https://zhuanlan.zhihu.com/p/45919661)
3. [ubuntu录屏软件-sha Betty的文章-知乎](https://zhuanlan.zhihu.com/p/231962019)
