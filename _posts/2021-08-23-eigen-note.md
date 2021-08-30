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

### 特殊矩阵向量赋值

若矩阵向量的大小确定，可不加行列数。

```cpp
// 创建对应类（作为等号右值）
MatrixXd::Identity(rows, cols)
MatrixXd::Zero(rows, cols)
MatrixXd::Ones(rows, cols)
MatrixXd::Random(rows, cols)
// 调用对应成员函数
C.setIdentity(rows, cols)
C.setZero(rows, cols)
C.setOnes(rows, cols)
C.setRandom(rows,c ols)
```

### 逐元素初始化

逐行填满。

```cpp
Eigen::Matrix3d A;
A << 1.0, 0.0, 0.0,
    0.0, 1.0, 0.0,
    0.0, 0.0, 1.0;
```

### 从内存中映射

```cpp
int data[4] = {1, 2, 3, 4};
// 初始化，data内容被复制到矩阵中
Matrix2i mat2x2(data);
// 映射，data内容随着矩阵内容变化
Matrix2i::Map(data) = 2 * mat2x2;
MatrixXi::Map(data, 2, 2) += mat2x2;
```

## 矩阵操作

### 取矩阵块

以下两种方法等价，均表示从当前矩阵`(i, j)`元素处开始，取大小为`(rows, cols)`的矩阵。

```cpp
P.block(i, j, rows, cols);
P.block<rows, cols>(i, j);
```

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
