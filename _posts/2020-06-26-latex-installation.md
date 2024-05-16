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

## 相关概念区别

1. TeX：Knuth开发的排版系统，提供排版语言，版本号不断接近圆周率$\pi$；
2. LaTeX：Lamport开发的基于TeX的排版系统，是对于TeX的高层封装；
3. 引擎：将TeX代码转换为页面描述语言（Page Description Language，PDL），类似C++的编译器，主要包括Plain TeX、pdfTeX、LuaTeX、**XeTeX（推荐）**、Tectonic等；
4. 发行版：将引擎、宏、宏包、编辑器等打包，主要包括MiKTeX、**TeXLive（推荐）**、MacTeX、CTeX等；
5. 编辑器：提供编辑环境，主要包括**TeXstudio（推荐）**、TeXworks、Overleaf等；

## Windows

1. 下载`texlive.iso`文件并挂载；
2. 以管理员身份运行`install-tl-windows.bat`；
3. 修改安装路径；
4. 取消勾选`安装TeXworks前端`；
5. `Advanced`->`Customize`->`Languages`，只勾选`Chinese`、`Chinese/Japanese/Korean(base)`、`US and UK English`三项，其余语言包不常用，取消安装可以节省安装空间；
6. `Advanced`->`Customize`->`Other collections`，确认只有`TeXworks editor`项未被勾选；
7. 安装TeXLive；
8. 安装TeXstudio；

## Ubuntu

1. 安装TeXLive：

    ```shell
    sudo apt install texlive-full
    ```

2. 安装TeXstudio：

    ```shell
    sudo apt install texstudio
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

1. [LaTeX引擎、格式、宏包、发行版大梳理-Rabbyt的文章-知乎](https://zhuanlan.zhihu.com/p/181557253)
2. [TeX家族（TeX, XeTeX, LuaTeX,XeLaTeX …看完这篇就懂了）-MOON学术论文写作的文章-知乎](https://zhuanlan.zhihu.com/p/248669482)
3. [LaTeX常见发行版与安装建议-LaTeX工作室](http://static.latexstudio.net/article/2019/0422/BeginLaTeX-Install-1.pdf)
4. [Page description language-Wikipedia](https://en.wikipedia.org/wiki/Page_description_language)
5. [tectonic-typesetting/tectonic](https://github.com/tectonic-typesetting/tectonic)
6. [TeXLive-清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)
7. [TeXstudio](http://texstudio.sourceforge.net/)
8. [最新TeXLive环境的安装与配置-cying的文章-知乎](https://zhuanlan.zhihu.com/p/41855480)
9. [Ubuntu18.04安装LaTeX并配置中文环境-CSDN博客](https://blog.csdn.net/qq_41814939/article/details/82288145)
10. [OsbertWang/install-latex-guide-zh-cn](https://github.com/OsbertWang/install-latex-guide-zh-cn)
