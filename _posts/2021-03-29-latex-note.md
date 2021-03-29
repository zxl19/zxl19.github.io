---
layout: post
title: LaTeX使用笔记
date: 2021-03-29
author: zxl19
tags: [LaTeX]
comments: true
toc: true
pinned: false
---

我的$\LaTeX$使用笔记及格式约定，供个人速查使用。

<!-- more -->

## 常用宏包

```latex
\usepackage{amsmath,amsthm,amsfonts,amssymb,amscd}  % 数学公式、符号等宏包
\usepackage{enumerate}      % 插入带序号列表
\usepackage{graphicx}       % 插入图片
\usepackage{listings}       % 插入代码块

\usepackage{hyperref}       % 插入超链接
\hypersetup{                % 超链接格式设置
    colorlinks=true,
    linkcolor=blue,
    linkbordercolor={0 0 1}
}

\usepackage{ctex}           % 中文支持
\usepackage{mathtools}      % 插入分段函数

\usepackage{algorithm}      % 插入伪代码
\usepackage{algpseudocode}  % 插入伪代码
\renewcommand{\algorithmicrequire}{\textbf{Input:}} % Use Input in the format of Algorithm
\renewcommand{\algorithmicensure}{\textbf{Output:}} % Use Output in the format of Algorithm

\usepackage[framed,numbered,autolinebreaks,useliterate]{mcode}  % 插入MATLAB代码块，基于listings开发
```

## 格式约定

1. 源码在遇到`\begin{}`时要缩进；
2. 数学符号参考[常用数学符号的 LaTeX 表示方法](https://mohu.org/info/symbols/symbols.htm)，但有以下几点注意事项：

    - 上下标使用`{}`括起来；
    - 矩阵和向量使用`\mathbf{}`；
    - 集合使用`\mathbb{}`；
    - 范数使用`\|`；
    - argmin使用`\mathop{\arg\min}\limits_{}`，argmax同理；
    - 小空格用`\quad`，大空格用`\qquad`；
    - 分式尽量使用`\dfrac{}{}`，若显示有问题再使用`\frac{}{}`；

3. 括号大小自动调整；

    ```latex
    \left(  \right)
    \left[  \right]
    \left{  \right}
    \left\| \right\|
    ```

## 列表

### 无序号

```latex
\begin{itemize} % 默认：实心点
    \item       默认样式
    \item[*]    指定样式
\end{itemize}
```

### 有序号

```latex
\begin{enumerate}[(1)] % 默认：1.
    \item 支持123
    \item 支持abc
    \item 支持ABC
    \item 支持i ii iii
    \item 支持I II III
    \item 在上述基础上支持左右括号
\end{enumerate}
```

## 公式

### 行内公式

```latex
$公式内容$
```

### 行间公式

#### 带编号

##### 单个公式

```latex
\begin{equation}
    \label{eq1.1}
    公式内容
\end{equation}
```

##### 多个公式

```latex
\begin{align}
    \label{eq1.2}
    & 公式内容
    \label{eq1.3}
    & 公式内容
\end{align}
```

##### 引用方式

```latex
\eqref{eq1.1}
```

#### 无编号

```latex
\begin{align*}
    & 公式内容
    & 公式内容
\end{align*}
```

#### 分段函数

```latex
\begin{equation}
    \label{eq1.4}
    \begin{dcases}
        公式内容 & 条件 \\
        公式内容 & 条件
    \end{dcases}
\end{equation}
```

1. dcases   条件中无文本
2. dcases*  条件中有文本

## 图片

## 表格

## 超链接

## 代码块

## 参考文献

TODO

内容：
==括号自调整==
==一些数学符号的约定==
==代码缩进==
序号
项目符号
公式（有编码无编码）
矩阵
表格
图片
超链接添加方式
分段函数
==宏（神经网络、mcode）==
==模板网站==
==有用的网站==

## 公式排版

1. 行内公式



2. 行间公式
    - 有编码

        ```latex
        \begin{equation}
		    \label{eq1.1}
            公式内容
	    \end{equation}
        ```

    - 无编码

        ```latex
        \begin{align*}
		    \label{eq1.1}
            公式内容
	    \end{align*}
        ```

## 常用网站

1. [Detexify](http://detexify.kirelabs.org/classify.html)
2. [Tables Generator](https://www.tablesgenerator.com/)
3. [公式王](https://gongshi.wang/)

## 常用模板

1. [CS310-Assignment Template](https://www.overleaf.com/latex/templates/cs310-assignment-template/qrqpndrxpcht)
2. [CheatSheet](https://www.latextemplates.com/template/cheatsheet)
3. [PlotNeuralNet](https://github.com/HarisIqbal88/PlotNeuralNet)

## 参考

1. [LaTeX 工作室](https://www.latexstudio.net/)
2. [Overleaf Templates](https://www.overleaf.com/latex/templates)
3. [LaTeX Templates](https://www.latextemplates.com)