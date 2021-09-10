---
layout: post
title: Eigen库使用笔记
date: 2021-08-23
author: zxl19
tags: [C++, Eigen, Note]
comments: true
toc: true
pinned: true
---

我的Eigen库使用笔记。

<!-- more -->

## Hello World

1. Eigen是纯头文件库；
2. `#include <Eigen/Eigen>`（全部模块功能）=`#include <Eigen/Dense>`（绝大部分模块功能）+`#include <Eigen/Sparse>`（稀疏矩阵模块功能）；
3. `#include <Eigen/Core>`为核心模块，包含`Matrix`类和`Array`类的定义、基础的线性代数操作等；
4. `#include <Eigen/Geometry>`为几何模块，包含SLAM相关的位姿表示、四元数、旋转向量等；
5. 对于MATLAB用户，可以参考[Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)快速入门，[zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)将其整理成Markdown和PDF文档；
6. `Matrix`模板类定义了矩阵和向量，用于进行线性代数运算；`Array`模板类定义了数组，用于进行类似MATLAB的逐元素操作；
7. Eigen使用`typedef`关键字重命名了常用大小的矩阵和数组，在使用中应尽可能少用动态大小的矩阵和数组，以提高运行速度；

    ```cpp
    // Matrix类
    Matrix<float,Dynamic,Dynamic>   <=>   MatrixXf
    Matrix<double,Dynamic,1>        <=>   VectorXd
    Matrix<int,1,Dynamic>           <=>   RowVectorXi
    Matrix<float,3,3>               <=>   Matrix3f
    Matrix<float,4,1>               <=>   Vector4f
    // Array类
    Array<float,Dynamic,Dynamic>    <=>   ArrayXXf
    Array<double,Dynamic,1>         <=>   ArrayXd
    Array<int,1,Dynamic>            <=>   RowArrayXi
    Array<float,3,3>                <=>   Array33f
    Array<float,4,1>                <=>   Array4f
    ```

8. `Matrix`类和`Array`类之间运算和类型转换的规则；

    ```cpp
    Array44f a1, a2;
    Matrix4f m1, m2;
    m1 = a1 * a2;                     // 逐元素相乘，运算结果从Array类到Matrix类隐式类型转换
    a1 = m1 * m2;                     // 矩阵相乘，运算结果从Matrix类到Array类隐式类型转换
    a2 = a1 + m1.array();             // Array类和Matrix类的对象在运算中禁止混用，需要显式类型转换
    m2 = a1.matrix() + m1;            // Array类和Matrix类的对象在运算中禁止混用，需要显式类型转换
    ArrayWrapper<Matrix4f> m1a(m1);   // m1a相当于m1.array()，二者参数相同
    MatrixWrapper<Array44f> a1m(a1);  // a1m相当于a1.matrix()，二者参数相同
    ```

9. `Matrix`类和`Array`类的初始化方式，建议在定义后对变量进行初始化；

    - 固定大小-大小确定，可不加行列数：

        ```cpp
        typedef {Matrix3f|Array33f} FixedXD;
        FixedXD x;
        // 创建对应类的对象（作为等号右值）
        x = FixedXD::Identity();
        x = FixedXD::Zero();
        x = FixedXD::Ones();
        x = FixedXD::Constant(value);
        x = FixedXD::Random();
        x = FixedXD::LinSpaced(size, low, high);
        // 调用对应成员函数
        x.setIdentity();
        x.setZero();
        x.setOnes();
        x.setConstant(value);
        x.setRandom();
        x.setLinSpaced(size, low, high);
        ```

    - 二维动态大小：

        ```cpp
        typedef {MatrixXf|ArrayXXf} Dynamic2D;
        Dynamic2D x;
        // 创建对应类的对象（作为等号右值）
        x = Dynamic2D::Identity(rows, cols);
        x = Dynamic2D::Zero(rows, cols);
        x = Dynamic2D::Ones(rows, cols);
        x = Dynamic2D::Constant(rows, cols, value);
        x = Dynamic2D::Random(rows, cols);
        // 调用对应成员函数
        x.setIdentity(rows, cols);
        x.setZero(rows, cols);
        x.setOnes(rows, cols);
        x.setConstant(rows, cols, value);
        x.setRandom(rows, cols);
        ```

    - 一维动态大小

        ```cpp
        typedef {VectorXf|ArrayXf} Dynamic1D;
        Dynamic1D x;
        // 创建对应类的对象（作为等号右值）
        x = Dynamic1D::Zero(size);
        x = Dynamic1D::Ones(size);
        x = Dynamic1D::Constant(size, value);
        x = Dynamic1D::Random(size);
        x = Dynamic1D::LinSpaced(size, low, high);
        // 调用对应成员函数
        x.setZero(size);
        x.setOnes(size);
        x.setConstant(size, value);
        x.setRandom(size);
        x.setLinSpaced(size, low, high);
        ```

## Matrix类

### 矩阵初始化

#### 初始化为特殊矩阵

```cpp
// 基向量
x = Vector3f::UnitX(); // 1 0 0
x = Vector3f::UnitY(); // 0 1 0
x = Vector3f::UnitZ(); // 0 0 1
x = Vector4f::Unit(i);
x.setUnit(i);
x = VectorXf::Unit(size, i);
x.setUnit(size, i);
```

#### 逐元素初始化

可以使用`<<`运算符逐行对于元素进行初始化，也可以使用下标对于特定元素进行初始化。

```cpp
Eigen::Matrix2d A;
A << 1.0, 0.0,
    0.0, 1.0;
A(0, 0) = 1.0;
A(0, 1) = 0.0;
A(1, 0) = 0.0;
A(1, 1) = 1.0;
Eigen::Vector2d b(1.0, 1.0);
b << 1.0, 1.0;
b(0) = 1.0;
b(1) = 1.0;
```

#### 从内存中映射

```cpp
float array[3];
// 映射，array内容随着矩阵内容变化
Vector3f::Map(array).fill(10);
int data[4] = {1, 2, 3, 4};
// 初始化，data内容被复制到矩阵中
Matrix2i mat2x2(data);
// 映射，data内容随着矩阵内容变化
Matrix2i::Map(data) = 2 * mat2x2;
MatrixXi::Map(data, 2, 2) += mat2x2;
```

### 矩阵操作

#### 计算大小

```cpp
// 向量长度
x.size()
// 矩阵行数、列数
C.rows()
C.cols()
```

#### 取矩阵行列

```cpp
P.row(i)
P.col(j)
```

#### 取矩阵块

以下两种方法等价，均表示从当前矩阵`(i, j)`元素处开始，取大小为`(rows, cols)`的矩阵。

```cpp
P.block(i, j, rows, cols)
P.block<rows, cols>(i, j)
```

#### 转置

```cpp
x.transpose()
C.transpose()
```

### 矩阵运算

#### 点乘和叉乘

```cpp
// 点乘
x.dot(y)
x.transpose() * y
// 叉乘
x.cross(y)
```

#### 奇异值分解

```cpp
Eigen::Matrix3f A;
Eigen::JacobiSVD<Eigen::Matrix3f> svd(A, Eigen::ComputeFullU | Eigen::ComputeFullV);
Eigen::Matrix3f U = svd.matrixU();
Eigen::Matrix3f V = svd.matrixV();
Eigen::Vector3f Sigma= svd.singularValues();
```

## Array类

### 逐元素运算

```cpp
array1.abs2()
array1.abs()
array1.sqrt()
array1.log()
array1.log10()
array1.exp()
array1.pow(array2)
array1.pow(scalar)

array1.square()
array1.cube()
array1.inverse()

array1.sin()
array1.cos()
array1.tan()
array1.asin()
array1.acos()
array1.atan()
array1.sinh()
array1.cosh()
array1.tanh()
array1.arg()

array1.floor()
array1.ceil()
array1.round()

array1.isFinite()
array1.isInf()
array1.isNaN()
```

## 位姿表示

TODO

### 位姿初始化

#### 四元数

#### 旋转向量

### 位姿相关运算

#### 旋转矩阵归一化

通过将旋转矩阵转换为四元数，将四元数归一化后再转回旋转矩阵。

```cpp
Eigen::Matrix3f R;
Eigen::Quaternionf q(R);
R = q.normalized().toRotationMatrix();
```

## 参考

1. [Eigen: Main Page](https://eigen.tuxfamily.org/dox/)
2. [Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)
3. [zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)
4. [[QuickRef] Dense matrix and array manipulations](https://eigen.tuxfamily.org/dox/group__QuickRefPage.html)
5. [[QuickRef] Sparse linear algebra](https://eigen.tuxfamily.org/dox/group__SparseQuickRefPage.html)
6. [SVD-CSDN博客](https://blog.csdn.net/jiang_he_hu_hai/article/details/78363642)
7. [旋转矩阵归一化1-Stack Overflow](https://stackoverflow.com/questions/21761909/eigen-convert-matrix3d-rotation-to-quaternion)
8. [旋转矩阵归一化2-Stack Overflow](https://stackoverflow.com/questions/43896041/eigen-matrix-to-quaternion-and-back-have-different-result)
