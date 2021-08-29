---
layout: post
title: Eigen库使用笔记
date: 2021-08-23
author: zxl19
tags: [C++, Eigen, Note]
comments: true
toc: true
pinned: false
---

我的Eigen库使用笔记。

<!-- more -->

## Hello World

1. Eigen是纯头文件库；
2. `#include <Eigen/Eigen>`（全部模块功能）=`#include <Eigen/Dense>`（绝大部分模块功能）+`#include <Eigen/Sparse>`（稀疏矩阵模块功能）；
3. 对于MATLAB用户，可以参考[Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)快速入门，[zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)将其整理成Markdown和PDF文档；

## 矩阵向量初始化

## 矩阵操作

### 旋转矩阵归一化

通过将旋转矩阵转换为四元数，将四元数归一化后再转回旋转矩阵。

```cpp
Eigen::Matrix3f R;
Eigen::Quaternionf q(R);
R = q.normalized().toRotationMatrix();
```

## 矩阵运算

### 奇异值分解

```cpp
Eigen::Matrix3f A;
Eigen::JacobiSVD<Eigen::Matrix3f> svd(A, Eigen::ComputeFullU | Eigen::ComputeFullV);
Eigen::Matrix3f U = svd.matrixU();
Eigen::Matrix3f V = svd.matrixV();
Eigen::Vector3f Sigma= svd.singularValues();
```

## 参考

1. [Eigen: Main Page](https://eigen.tuxfamily.org/dox/)
2. [Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)
3. [zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)
4. [旋转矩阵归一化1-Stack Overflow](https://stackoverflow.com/questions/21761909/eigen-convert-matrix3d-rotation-to-quaternion)
5. [旋转矩阵归一化2-Stack Overflow](https://stackoverflow.com/questions/43896041/eigen-matrix-to-quaternion-and-back-have-different-result)
6. [SVD-CSDN博客](https://blog.csdn.net/jiang_he_hu_hai/article/details/78363642)
