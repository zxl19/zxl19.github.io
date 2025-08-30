---
layout: post
title: 在Ubuntu系统中监控系统状态
date: 2023-11-20
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中监控系统状态。

<!-- more -->

## 使用`top`命令

## 使用`htop`命令

### 安装

```shell
sudo apt install htop
```

## 使用`nmon`命令

### 安装

```shell
sudo apt install nmon
```

## 使用`glances`命令

### 安装

```shell
python3 -m pip install --user glances
```

## 使用polybar状态栏

1. [polybar/polybar](https://github.com/polybar/polybar)

## 使用SysPeek

### 安装

```shell
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt update
sudo apt install syspeek
```

## 使用GNOME扩展

1. [paradoxxxzero/gnome-shell-system-monitor-applet](https://github.com/paradoxxxzero/gnome-shell-system-monitor-applet)
2. [eugene-rom/syspeek-gs](https://github.com/eugene-rom/syspeek-gs)

## 参考

1. [How to install Syspeek in Ubuntu-LinuxHelp](https://www.linuxhelp.com/how-to-install-syspeek-in-ubuntu-system-monitor-tool)
