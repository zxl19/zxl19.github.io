---
layout: post
title: Ceres库学习笔记
date: TODO
author: zxl19
tags: [C++, Ceres, Note]
comments: true
toc: true
pinned: false
---

我的Ceres库学习笔记。

<!-- more -->

## Ceres Hello World

1. Ceres是Google开发的非线性优化库，用于求解非线性最小二乘问题；
2. Ceres得名于谷神星，为了纪念高斯在1801年使用最小二乘法估计谷神星的位置；

## CMakeLists

## 求导方式

$$\begin{split}\min_{\mathbf{x}} &\quad \frac{1}{2}\sum_{i} \rho_i\left(\left\|f_i\left(x_{i_1}, ... ,x_{i_k}\right)\right\|^2\right) \\
\text{s.t.} &\quad l_j \le x_j \le u_j\end{split}$$

### 自动求导

### 解析求导

### 数值求导

不推荐使用

## 参考

1. [Ceres Solver](http://ceres-solver.org)
