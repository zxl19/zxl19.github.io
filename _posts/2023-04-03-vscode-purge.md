---
layout: post
title: 在Windows和Linux系统中完全卸载VS Code
date: 2023-04-03
author: zxl19
tags: [VS Code, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Linux系统中完全卸载VS Code。

<!-- more -->

## 背景

近期发现VS Code无法进行全局搜索，只能搜索项目根目录下的文件以及在编辑器中打开的文件中的内容。经过排查发现加密软件禁止了`rg`搜索工具，而VS Code依赖`rg`搜索工具实现全局搜索。在定位问题的过程中对于VS Code进行了完全卸载和重装。

1. [Search Issues](https://github.com/microsoft/vscode/wiki/Search-Issues)
2. [VS Code Find in Files not working (searching only in open files) #116637](https://github.com/microsoft/vscode/issues/116637)

## 完全卸载

### Windows

1. 卸载VS Code；
2. 删除扩展安装目录，删除`C:\Users\用户名\.vscode`文件夹；
3. 删除配置文件目录，删除`C:\Users\用户名\AppData\Roaming\Code`文件夹；

### Ubuntu

```shell
# 卸载
sudo apt purge code
sudo apt clean
sudo apt autoclean
sudo apt autoremove
# 删除扩展安装目录
cd ~ && rm -rf .vscode
# 删除配置文件目录
cd ~/.config && rm -rf Code
# 重启
reboot
```

## 重装

1. 通过官网下载安装包，将下载链接中的`az764295.vo.msecnd.net`改为`vscode.cdn.azure.cn`可以提高下载速度；
2. 通过`apt`安装：

    ```shell
    sudo apt install code
    ```

## 参考

1. [deepin下彻底删除vscode并重装，及一些配置-黄小跑的文章-知乎](https://zhuanlan.zhihu.com/p/148671055)
2. [完全卸载VSCode的方法-CSDN博客](https://blog.csdn.net/why_not_can/article/details/114315469)
3. [国内下载vscode速度慢问题解决-CozySun的文章-知乎](https://zhuanlan.zhihu.com/p/112215618)
