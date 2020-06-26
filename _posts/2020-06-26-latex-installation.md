---
layout: post
title: 在Windows和Ubuntu系统下安装LaTeX发行版
date: 2020-06-25
author: zxl19
tags: [LaTeX]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统下安装LaTeX发行版TeXLive。

<!-- more -->

## Windows

1. 下载.iso文件并挂载；
2. 以管理员身份运行`install-tl-windows.bat`；
3. 修改安装路径；
4. 取消勾选`安装TeXworks前端`；
5. Advanced
6. Advanced

## Ubuntu

1. 安装LaTeX发行版；

```shell
sudo apt-get install texlive-full
```

2. 安装编辑器texstudio。

```shell
sudo apt-get install texstudio
```

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
2. [最新TeXLive环境的安装与配置-cying的文章-知乎](https://zhuanlan.zhihu.com/p/41855480)
3. [CSDN博客](https://blog.csdn.net/qq_41814939/article/details/82288145)
