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

## Eigen Hello World

1. Eigen是纯头文件库；
2. Eigen各模块功能可查询[[QuickRef] Dense matrix and array manipulations](https://eigen.tuxfamily.org/dox/group__QuickRefPage.html)；
3. `#include <Eigen/Eigen>`（全部模块功能）=`#include <Eigen/Dense>`（绝大部分模块功能）+`#include <Eigen/Sparse>`（稀疏矩阵模块功能）；
4. `#include <Eigen/Core>`为核心模块，包含`Matrix`类和`Array`类的定义、基础的线性代数操作等；
5. `#include <Eigen/Geometry>`为几何模块，包含SLAM相关的位姿表示、四元数、旋转向量等；
6. 对于MATLAB用户，可以参考[Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)快速入门，[zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)将其整理成Markdown和PDF文档；
7. `Matrix`模板类定义了矩阵和向量，用于进行线性代数运算；`Array`模板类定义了数组，用于进行类似MATLAB的逐元素操作；
8. Eigen使用`typedef`关键字重命名了常用大小的矩阵和数组，后缀`f`代表`float`、`d`代表`double`、`i`代表`int`，在使用中应尽可能少用动态大小的矩阵和数组，以提高运行速度：

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

9. `Matrix`类和`Array`类之间运算和类型转换的规则：

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

10. `Matrix`类和`Array`类的初始化方式，建议在定义后对变量进行初始化；

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

    - 一维动态大小：

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

可以使用`<<`运算符逐行对于元素进行初始化，也可以使用下标对于特定元素进行初始化：

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

以下两种方式等价，均表示从当前矩阵`(i, j)`元素处开始，取大小为`(rows, cols)`的矩阵：

```cpp
P.block(i, j, rows, cols)
P.block<rows, cols>(i, j)
```

#### 转置

```cpp
x.transpose()
C.transpose()
```

#### 求和

```cpp
x.sum()
C.sum()
```

#### 取模

```cpp
x.norm()            // 取模
x.squaredNorm()     // 模的平方
```

### 矩阵运算

#### 方阵相关

```cpp
C.trace()           // 迹
C.inverse()         // 逆
C.determinant()     // 行列式
```

#### 点乘和叉乘

```cpp
// 点乘
x.dot(y)
x.transpose() * y
// 叉乘
x.cross(y)
```

#### 求解Ax=b形式线性方程组

```cpp
x = A.inverse() * b;                    // 直接求逆，速度最慢
x = A.colPivHouseholderQr().solve(b);   // 列主元QR分解
x = A.llt().solve(b);                   // Cholesky分解，要求正定阵
x = A.ldlt().solve(b);                  // LDLT分解，要求正定阵或非负定阵
```

全部求解方法及其对于矩阵要求、求解速度、求解精度对比：[Linear algebra and decompositions](https://eigen.tuxfamily.org/dox/group__TutorialLinearAlgebra.html)。

#### 特征值计算

```cpp
Eigen::Matrix3f A;
// 初始化方式1
EigenSolver<Matrix3d> eigen_solver(A);
// 初始化方式2，可用于计算多个矩阵的特征值
EigenSolver<Matrix3d> eigen_solver;
eigen_solver.compute(A)
// 查看计算结果方式
eigen_solver.eigenvalues()      // 特征值
eigen_solver.eigenvectors()     // 特征向量
// 实对称矩阵可以保证对角化成功，初始化方式和查看计算结果方式与上面相同
SelfAdjointEigenSolver<Matrix3d> eigen_solver(A.transpose() * A);
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

旋转向量、四元数表示的位姿可以直接当做旋转矩阵参与运算，因为重载了乘法运算符。

不同表示方式的位姿在赋值时需要进行显式类型转换。

### 位姿初始化

#### 旋转向量

旋转向量并不是为了储存旋转，而是为了更加方便地创建其他类型的旋转。

旋转轴必须是单位向量，推荐使用基向量。

示例：

```cpp
// 3D旋转矩阵直接使用Eigen::Matrix3d或Eigen::Matrix3f
Eigen::Matrix3d rotation_matrix = Eigen::Matrix3d::Identity();
// 旋转向量使用AngleAxis，其底层不直接是Matrix类，但运算可以当作矩阵（因为重载了运算符）
Eigen::AngleAxisd rotation_vector(M_PI / 4, Vector3d(0, 0, 1)); // 沿Z轴旋转45度
rotation_matrix = rotation_vector.matrix();                     // 旋转向量转旋转矩阵
rotation_matrix = rotation_vector.toRotationMatrix();           // 旋转向量转旋转矩阵
// 用AngleAxis进行坐标变换
Eigen::Vector3d v(1, 0, 0);
Eigen::Vector3d v_rotated = rotation_vector * v;
// 相当于用旋转矩阵进行坐标变换
Eigen::Vector3d v_rotated = rotation_matrix * v;
```

#### 欧拉角

示例：

```cpp
// 欧拉角转旋转矩阵，借助旋转向量
Eigen::AngleAxisd roll_vector(roll_rad, Eigen::Vector3d::UnitX());
Eigen::AngleAxisd pitch_vector(pitch_rad, Eigen::Vector3d::UnitY());
Eigen::AngleAxisd yaw_vector(yaw_rad, Eigen::Vector3d::UnitZ());
Eigen::Matrix3d rotation_matrix = (roll_vector * pitch_vector * yaw_vector).toRotationMatrix();
// 旋转矩阵转欧拉角
Eigen::Vector3d euler_angles = rotation_matrix.eulerAngles(2, 1, 0);    // ZYX顺序，即yaw-pitch-roll顺序
```

#### 四元数

必须使用单位四元数表示旋转。

示例：

```cpp
// 直接初始化，注意参数顺序为(w，x，y，z)
Eigen::Quaterniond q = Eigen::Quaterniond(q_w, q_x, q_y, q_z);
// 可以把AngleAxis赋值给四元数，反之亦然
Eigen::Quaterniond q = Eigen::Quaterniond(rotation_vector);
// 可以把旋转矩阵赋值给四元数
Eigen::Quaterniond q = Eigen::Quaterniond(rotation_matrix);
// 访问四元数中各元素
q.x()
q.y()
q.z()
q.w()
q.coeffs()              // 注意coeffs的顺序是(x, y, z, w)，w为实部，前三者为虚部，这也是Eigen中四元数的存储顺序
q.normalize()           // 归一化四元数，直接对原四元数操作，无返回值，不能作为等号右值
q.normalized()          // 归一化四元数，原四元数不变，返回拷贝构造值，可以作为等号右值
q.matrix()              // 四元数转旋转矩阵
q.toRotationMatrix()    // 四元数转旋转矩阵
// 使用四元数旋转一个向量，使用重载的乘法即可
v_rotated = q * v;      // 注意数学上是qvq^{-1}
```

#### 欧式变换

示例：

```cpp
// 欧氏变换矩阵使用 Eigen::Isometry
Eigen::Isometry3d T = Eigen::Isometry3d::Identity();    // 虽然称为3d，实质上是4*4的矩阵
T.rotate(rotation_vector);                              // 按照rotation_vector进行旋转
T.pretranslate(Vector3d(1, 2, 3))                       // 把平移向量设成(1, 2, 3)
T.matrix()                                              // 欧氏变换矩阵
// 用欧氏变换矩阵进行坐标变换
Eigen::Vector3d v_transformed = T * v;                  // 相当于R * v + t
```

### 位姿相关运算

#### 旋转矩阵归一化

1. 四元数法：

    通过将旋转矩阵转换为四元数，将四元数归一化后再转回旋转矩阵。

    ```cpp
    Eigen::Matrix3f R;
    Eigen::Quaternionf q(R);
    R = q.normalized().toRotationMatrix();
    ```

2. SVD分解法：

    ```cpp
    Eigen::Matrix3f R;
    Eigen::JacobiSVD<Eigen::MatrixXf> svd(R, Eigen::ComputeFullU | Eigen::ComputeFullV);
    R = svd.matrixU() * svd.matrixV().transpose();
    ```

3. 流形投影法：

    ```cpp
    Eigen::Matrix3f R;
    Eigen::Matrix3f H = R * R.transpose();
    Eigen::Matrix3f L = H.llt().matrixL();
    R = L.inverse() * R;
    ```

## 参考

1. [Eigen: Main Page](https://eigen.tuxfamily.org/dox/)
2. [[QuickRef] Dense matrix and array manipulations](https://eigen.tuxfamily.org/dox/group__QuickRefPage.html)
3. [[QuickRef] Sparse linear algebra](https://eigen.tuxfamily.org/dox/group__SparseQuickRefPage.html)
4. [Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)
5. [zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)
6. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
7. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
8. [Linear algebra and decompositions](https://eigen.tuxfamily.org/dox/group__TutorialLinearAlgebra.html)
9. [LU分解、LDLT分解和Cholesky分解-CSDN博客](https://blog.csdn.net/zhouliyang1990/article/details/21952485)
10. [SVD-CSDN博客](https://blog.csdn.net/jiang_he_hu_hai/article/details/78363642)
11. [四元数归一化1-Stack Overflow](https://stackoverflow.com/questions/48019329/difference-between-norm-normalize-and-normalized-in-eigen)\
12. [四元数归一化2-CSDN博客](https://blog.csdn.net/m0_56348460/article/details/117386857)
13. [旋转矩阵归一化1-Stack Overflow](https://stackoverflow.com/questions/21761909/eigen-convert-matrix3d-rotation-to-quaternion)
14. [旋转矩阵归一化2-Stack Overflow](https://stackoverflow.com/questions/43896041/eigen-matrix-to-quaternion-and-back-have-different-result)
