---
layout: post
title: 在Windows和Ubuntu系统中安装LaTeX发行版
date: 2020-06-26
author: zxl19
tags: [LaTeX, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统中安装LaTeX发行版TeXLive。

<!-- more -->

## Windows

1. 下载`texlive.iso`文件并挂载；
2. 以管理员身份运行`install-tl-windows.bat`；
3. 修改安装路径；
4. 取消勾选`安装TeXworks前端`；
5. `Advanced->Customize->Languages`，只勾选`Chinese`、`Chinese/Japanese/Korean(base)`、`US and UK English`三项，其余语言包不常用，取消安装可以节省安装空间；
6. `Advanced->Customize->Other collections`，确认只有`TeXworks editor`项未被勾选；
7. 安装TeXLive；
8. 安装TeXstudio；

## Ubuntu

1. 安装LaTeX发行版：

    ```shell
    sudo apt-get install texlive-full
    ```

2. 安装编辑器TeXstudio：

    ```shell
    sudo apt-get install texstudio
    ```

## 在线使用

1. 使用[Overleaf](https://www.overleaf.com)；
2. 注册账号即可使用；
3. 如果网络连接不上可以使用[Overleaf中文版](https://cn.overleaf.com)；

## 编译测试

```latex
%!TEX program = xelatex
\documentclass{article}
\usepackage{xeCJK}
\begin{document}
    Hello \LaTeX  world!

    你好！
\end{document}
```

## 参考

1. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)
2. [TeXstudio](http://texstudio.sourceforge.net/)
3. [最新TeXLive环境的安装与配置-cying的文章-知乎](https://zhuanlan.zhihu.com/p/41855480)
4. [Ubuntu安装-CSDN博客](https://blog.csdn.net/qq_41814939/article/details/82288145)
5. [Overleaf](https://www.overleaf.com)
6. [Overleaf Chinese](https://cn.overleaf.com)
