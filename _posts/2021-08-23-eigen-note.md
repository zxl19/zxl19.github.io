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
2. Eigen稠密矩阵和数组模块功能可以查询[[QuickRef] Dense matrix and array manipulations](https://eigen.tuxfamily.org/dox/group__QuickRefPage.html)；
3. Eigen稀疏线性代数模块功能可以查询[[QuickRef] Sparse linear algebra](https://eigen.tuxfamily.org/dox/group__SparseQuickRefPage.html)；
4. `#include <Eigen/Eigen>`（全部模块功能）=`#include <Eigen/Dense>`（绝大部分模块功能）+`#include <Eigen/Sparse>`（稀疏矩阵模块功能）；
5. `#include <Eigen/Core>`为核心模块，包含`Matrix`类和`Array`类的定义、基础的线性代数操作等；
6. `#include <Eigen/Geometry>`为几何模块，包含SLAM相关的位姿表示、四元数、旋转向量等；
7. 对于MATLAB用户，可以参考[Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)快速入门，[zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)将其整理成Markdown和PDF文档；
8. `Matrix`模板类定义了矩阵和向量，用于进行线性代数运算；`Array`模板类定义了数组，用于进行类似MATLAB的逐元素操作；
9. Eigen使用`typedef`关键字重命名了常用大小的矩阵和数组，后缀`f`代表`float`、`d`代表`double`、`i`代表`int`，不同精度的矩阵在运算中禁止混用，需要显式类型转换，在使用中应尽可能少用动态大小的矩阵和数组，以提高运行速度：

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

10. `Matrix`类和`Array`类之间运算和类型转换的规则：

    ```cpp
    Array44f a1, a2;
    Matrix4f m1, m2;
    m1 = a1 * a2;                       // 逐元素相乘，运算结果从Array类到Matrix类隐式类型转换
    a1 = m1 * m2;                       // 矩阵相乘，运算结果从Matrix类到Array类隐式类型转换
    a2 = a1 + m1.array();               // Array类和Matrix类的对象在运算中禁止混用，需要显式类型转换
    m2 = a1.matrix() + m1;              // Array类和Matrix类的对象在运算中禁止混用，需要显式类型转换
    ArrayWrapper<Matrix4f> m1a(m1);     // m1a相当于m1.array()，二者参数相同
    MatrixWrapper<Array44f> a1m(a1);    // a1m相当于a1.matrix()，二者参数相同
    ```

11. `Matrix`类和`Array`类的初始化方式，建议在定义后对变量进行初始化；

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

#### 转置

```cpp
// 以矩阵为例，向量同理
// 转置
C.transpose()
C.transposeInPlace()    // in-place version
// 共轭转置
C.adjoint()
C.adjointInPlace()      // in-place version
```

在使用矩阵的转置给自身赋值时需要避免混淆现象（aliasing）：

```cpp
// 错误，存在混淆现象
C = C.transpose();
C = C.adjoint();
// 正确，避免混淆现象
C = C.transposeInPlace();
C = C.adjointInPlace();
```

#### 求和

```cpp
// 以矩阵为例，向量同理
C.sum()
```

#### 取模

```cpp
x.norm()            // 取模
x.squaredNorm()     // 模的平方
```

#### 类型转换

```cpp
// 以矩阵为例，向量同理
C.cast<double>()    // 转为double类型
C.cast<float>()     // 转为float类型
C.cast<int>()       // 转为int类型
C.real()            // 逐元素取实部
C.imag()            // 逐元素取虚部
C.conjugate()       // 逐元素取共轭
```

#### 改变大小

```cpp
// 改变大小后删除原有数据
// 向量
vector.resize(size);
// 矩阵
matrix.resize(nb_rows, nb_cols);
matrix.resize(Eigen::NoChange, nb_cols);
matrix.resize(nb_rows, Eigen::NoChange);
// 改变大小后保留原有数据
// 向量
vector.resizeLike(other_vector);
vector.conservativeResize(size);
// 矩阵
matrix.resizeLike(other_matrix);
matrix.conservativeResize(nb_rows, nb_cols);
```

#### 分块

```cpp
// 向量
// Eigen                           // MATLAB
x.head(n)                          // x(1:n)
x.head<n>()                        // x(1:n)
x.tail(n)                          // x(end - n + 1: end)
x.tail<n>()                        // x(end - n + 1: end)
x.segment(i, n)                    // x(i+1 : i+n)
x.segment<n>(i)                    // x(i+1 : i+n)
// 矩阵
// Eigen                           // MATLAB
P.block(i, j, rows, cols)          // P(i+1 : i+rows, j+1 : j+cols)
P.block<rows, cols>(i, j)          // P(i+1 : i+rows, j+1 : j+cols)
P.row(i)                           // P(i+1, :)
P.col(j)                           // P(:, j+1)
P.leftCols<cols>()                 // P(:, 1:cols)
P.leftCols(cols)                   // P(:, 1:cols)
P.middleCols<cols>(j)              // P(:, j+1:j+cols)
P.middleCols(j, cols)              // P(:, j+1:j+cols)
P.rightCols<cols>()                // P(:, end-cols+1:end)
P.rightCols(cols)                  // P(:, end-cols+1:end)
P.topRows<rows>()                  // P(1:rows, :)
P.topRows(rows)                    // P(1:rows, :)
P.middleRows<rows>(i)              // P(i+1:i+rows, :)
P.middleRows(i, rows)              // P(i+1:i+rows, :)
P.bottomRows<rows>()               // P(end-rows+1:end, :)
P.bottomRows(rows)                 // P(end-rows+1:end, :)
P.topLeftCorner(rows, cols)        // P(1:rows, 1:cols)
P.topRightCorner(rows, cols)       // P(1:rows, end-cols+1:end)
P.bottomLeftCorner(rows, cols)     // P(end-rows+1:end, 1:cols)
P.bottomRightCorner(rows, cols)    // P(end-rows+1:end, end-cols+1:end)
P.topLeftCorner<rows,cols>()       // P(1:rows, 1:cols)
P.topRightCorner<rows,cols>()      // P(1:rows, end-cols+1:end)
P.bottomLeftCorner<rows,cols>()    // P(end-rows+1:end, 1:cols)
P.bottomRightCorner<rows,cols>()   // P(end-rows+1:end, end-cols+1:end)
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

#### 逐元素运算

1. `Matrix`类可以通过调用对应成员函数实现逐元素运算，此时返回值类型为`Matrix`类：

    ```cpp
    mat1.cwiseMin(mat2)                 mat1.cwiseMin(scalar)
    mat1.cwiseMax(mat2)                 mat1.cwiseMax(scalar)
    mat1.cwiseAbs2()
    mat1.cwiseAbs()
    mat1.cwiseSqrt()
    mat1.cwiseInverse()
    mat1.cwiseProduct(mat2)
    mat1.cwiseQuotient(mat2)
    mat1.cwiseEqual(mat2)               mat1.cwiseEqual(scalar)
    mat1.cwiseNotEqual(mat2)
    ```

2. 也可以将`Matrix`类转换为`Array`类后调用对应成员函数实现逐元素运算，此时返回值类型为`Array`类：

    ```cpp
    mat1.array().min(mat2.array())      mat1.array().min(scalar)
    mat1.array().max(mat2.array())      mat1.array().max(scalar)
    mat1.array().abs2()
    mat1.array().abs()
    mat1.array().sqrt()
    mat1.array().inverse()
    mat1.array() * mat2.array()
    mat1.array() / mat2.array()
    mat1.array() == mat2.array()        mat1.array() == scalar
    mat1.array() != mat2.array()
    ```

#### 求解Ax=b形式线性方程组

Eigen提供的全部稠密矩阵分解方法及其特性和数值稳定性可以参考[Catalogue of dense decompositions](https://eigen.tuxfamily.org/dox/group__TopicLinearAlgebraDecompositions.html)。

##### 有解析解

```cpp
x = A.inverse() * b;                    // 直接求逆，速度最慢
x = A.partialPivLu().solve(b);          // 部分主元LU分解，要求可逆阵
x = A.colPivHouseholderQr().solve(b);   // 列主元QR分解
x = A.llt().solve(b);                   // Cholesky分解，要求正定阵
x = A.ldlt().solve(b);                  // LDLT分解，要求正定阵或非负定阵
```

1. Eigen提供的全部求解方法及其对于矩阵要求、求解速度、求解精度的对比可以参考[Linear algebra and decompositions](https://eigen.tuxfamily.org/dox/group__TutorialLinearAlgebra.html)；
2. Eigen提供的全部求解方法及其在不同大小矩阵下求解速度的定量对比可以参考[Benchmark of dense decompositions](https://eigen.tuxfamily.org/dox/group__DenseDecompositionBenchmark.html)；

##### 无解析解

求解最小二乘问题：

1. Eigen提供的三种求解方法可以参考[Solving linear least squares systems](http://www.eigen.tuxfamily.org/dox/group__LeastSquares.html)；
2. 三种求解方法及其求解速度和求解精度的对比：

    | 求解方法 | 求解速度 | 求解精度 |
    | :--- | :--- | :---|
    | SVD分解 | 低 | 高 |
    | 列主元QR分解 | 中 | 中 |
    | 求解正规方程 | 高 | 低 |

```cpp
x = A.bdcSvd(Eigen::ComputeThinU | Eigen::ComputeThinV).solve(b);   // SVD分解
x = A.colPivHouseholderQr().solve(b);                               // 列主元QR分解
x = (A.transpose() * A).ldlt().solve(A.transpose() * b);            // 求解正规方程
relative_error = (A * x - b).norm() / b.norm();                     // L2范数相对误差
```

#### 特征值计算

```cpp
Eigen::Matrix3f A;
// 初始化方式1
EigenSolver<Eigen::Matrix3f> eigen_solver(A);
// 初始化方式2，可用于计算多个矩阵的特征值
EigenSolver<Eigen::Matrix3f> eigen_solver;
eigen_solver.compute(A);
if (eigen_solver.info() == Eigen::Success) {
    // 计算成功
    Eigen::Vector3f eigen_value = eigen_solver.eigenvalues();   // 特征值
    Eigen::Matrix3f eigen_vector = eigen_solver.eigenvectors(); // 特征向量
} else if (eigen_solver.info() == Eigen::NoConvergence) {
    // 计算失败
    std::cout << "Computation Failed!" << std::endl;
}
// 实对称矩阵可以保证对角化成功，初始化方式和查看计算结果方式与上面相同
SelfAdjointEigenSolver<Eigen::Matrix3f> eigen_solver(A.transpose() * A);
```

#### 奇异值分解

```cpp
// 方阵
Eigen::Matrix3f A;
// A = USV*
// 参数Eigen::ComputeFullU和Eigen::ComputeFullV分别表示计算方阵U和方阵V
// 此时奇异值矩阵S为方阵
Eigen::JacobiSVD<Eigen::Matrix3f> svd(A, Eigen::ComputeFullU | Eigen::ComputeFullV);
Eigen::Matrix3f U = svd.matrixU();
Eigen::Matrix3f V = svd.matrixV();
Eigen::Vector3f sv = svd.singularValues();
// 非方阵
Eigen::MatrixXf A;
// A = USV*
// 参数Eigen::ComputeFullU和Eigen::ComputeFullV分别表示计算方阵U和方阵V
// 此时奇异值矩阵S为非方阵
Eigen::JacobiSVD<Eigen::MatrixXf> svd(A, Eigen::ComputeFullU | Eigen::ComputeFullV);
// 参数Eigen::ComputeThinU和Eigen::ComputeThinV分别表示计算非方阵U和非方阵V
// 此时奇异值矩阵S为方阵
Eigen::JacobiSVD<Eigen::MatrixXf> svd(A, Eigen::ComputeThinU | Eigen::ComputeThinV);
Eigen::MatrixXf U = svd.matrixU();
Eigen::MatrixXf V = svd.matrixV();
Eigen::VectorXf sv = svd.singularValues();
```

## Array类

### 逐元素运算

包括算术运算符、比较运算符、常用数学函数等：

```cpp
array1.abs2()
array1.abs()                  abs(array1)
array1.sqrt()                 sqrt(array1)
array1.log()                  log(array1)
array1.log10()                log10(array1)
array1.exp()                  exp(array1)
array1.pow(array2)            pow(array1,array2)
array1.pow(scalar)            pow(array1,scalar)
                              pow(scalar,array2)
array1.square()
array1.cube()
array1.inverse()

array1.sin()                  sin(array1)
array1.cos()                  cos(array1)
array1.tan()                  tan(array1)
array1.asin()                 asin(array1)
array1.acos()                 acos(array1)
array1.atan()                 atan(array1)
array1.sinh()                 sinh(array1)
array1.cosh()                 cosh(array1)
array1.tanh()                 tanh(array1)
array1.arg()                  arg(array1)

array1.floor()                floor(array1)
array1.ceil()                 ceil(array1)
array1.round()                round(aray1)

array1.isFinite()             isfinite(array1)
array1.isInf()                isinf(array1)
array1.isNaN()                isnan(array1)
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

## Eigen中的内存对齐问题

### 内存对齐与向量化运算

1. 内存对齐是向量化运算（vectorization）的前提；
2. 向量化运算指的是使用单指令多数据流（Single Instruction Multiple Data，SIMD）指令集，实现一条指令对多个操作数的运算，进而实现运算加速；
3. 常用的SIMD指令集包括SSE（Streaming SIMD Extensions）、AVX（ Advanced Vector Extensions）等，其中SSE的操作数要求16字节对齐，AVX的操作数要求32字节对齐；

### 固定大小可向量化的Eigen对象

1. Eigen将编译时大小固定，并且大小是16字节的整数倍的对象称为固定大小可向量化的（fixed-size vectorizable），主要包括：

    ```cpp
    Eigen::Vector2d
    Eigen::Vector4d
    Eigen::Vector4f
    Eigen::Matrix2d
    Eigen::Matrix2f
    Eigen::Matrix4d
    Eigen::Matrix4f
    Eigen::Affine3d
    Eigen::Affine3f
    Eigen::Quaterniond
    Eigen::Quaternionf
    ```

2. 目前向量化运算支持128位数据包（例如SSE、AltiVec）、256位数据包（例如AVX）、512位数据包（例如AVX512），分别对应16字节、32字节、64字节，对于这些大小的数据包读写效率最高，因此对于固定大小可向量化的Eigen对象进行内存对齐有利于提高运算效率；

### 包含Eigen对象的类和结构体

1. 对于包含固定大小可向量化的Eigen对象的类和结构体，如果需要使用`new`关键字进行动态内存分配，则需要将宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW`声明为类和结构体的公有成员，这样在动态内存分配时会自动进行内存对齐：

    ```cpp
    class Foo {
     private:
      Eigen::Vector4d v;

     public:
      EIGEN_MAKE_ALIGNED_OPERATOR_NEW
    };

    Foo* foo = new Foo;
    ```

    - 如果使用C++17标准进行编译则不需要上述操作，因为C++17标准有对于超出默认对齐尺寸（over-aligned）数据的动态内存分配机制；
    - 在C++17标准下，宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW`定义为空；
    - 尽量将类和结构体中的Eigen对象声明一起放在类和结构体的开头，这并不是Eigen内存对齐的强制要求，但是可以节省内存对齐的空间；
    - 动态大小的Eigen对象自动进行动态内存分配，自动进行内存对齐，不需要上述操作；

2. 如果需要根据模板参数进行条件判断是否使用内存对齐，则需要使用宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW_IF`进行判断：

    ```cpp
    template<int n>
    class Foo {
      typedef Eigen::Matrix<float, n, 1> Vector;
      enum { NeedsToAlign = (sizeof(Vector) % 16) == 0 };
      Vector v;
     public:
      EIGEN_MAKE_ALIGNED_OPERATOR_NEW_IF(NeedsToAlign)
    };

    Foo<4> *foo4 = new Foo<4>; // foo4 is guaranteed to be 128bit-aligned
    Foo<3> *foo3 = new Foo<3>; // foo3 has only the system default alignment guarantee
    ```

    - 在参数`NeedsToAlign`为真时，自动添加宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW`进行内存对齐；
    - 如果使用C++17标准进行编译则不需要上述操作，因为C++17标准有对于超出默认对齐尺寸数据的动态内存分配机制；
    - 在C++17标准下，宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW_IF`定义为空；

3. 如果不想在多处声明宏`EIGEN_MAKE_ALIGNED_OPERATOR_NEW`，可以通过以下两个方法：

    - 使用`Eigen::DontAlign`关闭内存对齐，但是这会带来加载和存储上的额外耗时，具体影响程度主要取决于硬件：

        ```cpp
        class Foo {
         private:
          Eigen::Matrix<double, 4, 1, Eigen::DontAlign> v;
        }

    - 将固定大小可向量化的Eigen对象指针声明为类和结构体的私有成员，在创建类和结构体的对象时动态分配内存，优点是类和结构体不受到内存对齐的影响，缺点是需要额外的堆（heap）分配：

        ```cpp
        struct Foo_d {
          EIGEN_MAKE_ALIGNED_OPERATOR_NEW
          Vector4d v;
        };

        struct Foo {
          Foo() { init_d(); }
          ~Foo() { delete d; }
          void bar() {
            // use d->v instead of v
          }
         private:
          void init_d() { d = new Foo_d; }
          Foo_d* d;
        };
        ```

### 包含Eigen对象的STL容器

1. 对于包含固定大小可向量化的Eigen对象的STL容器，需要使用超出默认对齐尺寸的堆内存管理器（over-aligned allocator）`Eigen::aligned_allocator`进行内存对齐：

    ```cpp
    std::map<int, Eigen::Vector4d, std::less<int>, Eigen::aligned_allocator<std::pair<const int, Eigen::Vector4d> > >
    ```

    - `std::less`是`std::map`默认的排序函数，但是在这里为了指定堆内存管理器类型需要在其之前指定；
    - 如果使用C++17标准进行编译则不需要上述操作，因为C++17标准有对于超出默认对齐尺寸数据的动态内存分配机制；

2. 如果需要使用`std::vector`，除了需要使用堆内存管理器`Eigen::aligned_allocator`，还需要引入头文件`#include <Eigen/StdVector>`进行内存对齐：

    ```cpp
    #include <Eigen/StdVector>

    std::vector<Eigen::Vector4f, Eigen::aligned_allocator<Eigen::Vector4f> >
    ```

    - C++11之前的标准在调用`std::vector`的`resize()`成员函数时会调用元素的默认构造函数，造成元素的值传递，会破坏内存对齐；
    - 如果使用C++11以后的标准进行编译则不需要上述操作，因为C++11标准修复了之前标准中`std::vector`存在的问题；

3. 如果需要根据模板参数进行条件判断`std::vector`是否使用内存对齐，则需要使用宏`EIGEN_DEFINE_STL_VECTOR_SPECIALIZATION`进行判断：

    ```cpp
    #include<Eigen/StdVector>

    EIGEN_DEFINE_STL_VECTOR_SPECIALIZATION(Eigen::Matrix2d)
    std::vector<Eigen::Vector2d>
    ```

    - 如果使用C++11以后的标准进行编译则不需要上述操作，因为C++11标准修复了之前标准中`std::vector`存在的问题；
    - 优点是不需要在多处指定堆内存管理器`Eigen::aligned_allocator`，缺点是需要在每次声明`std::vector`前声明宏`EIGEN_DEFINE_STL_VECTOR_SPECIALIZATION`，否则会使用默认堆内存管理器`std::allocator`造成程序崩溃；

### 将Eigen对象作为函数参数传递

1. 从C++的角度，不建议使用值传递，因为会调用拷贝构造函数，对于大对象较为耗时，建议使用引用传递，如果不需要修改函数参数，建议使用常引用传递；
2. 从Eigen的角度，在将固定大小可向量化的Eigen对象作为函数参数传递时，不能使用值传递，应当使用引用传递，如果不需要修改函数参数，建议使用常引用传递；

    ```cpp
    void my_function(Eigen::Vector2d v);        // 错误
    void my_function(const Eigen::Vector2d& v); // 正确
    ```

    ```cpp
    struct Foo {
      Eigen::Vector2d v;
    };

    void my_function(Foo v);                    // 错误
    void my_function(const Foo& v);             // 正确
    ```

    - 原因是在值传递的过程中不考虑Eigen对象的内存对齐修饰符（alignment modifier）；
    - Eigen对象作为函数返回值不受影响；

## 参考

1. [Eigen: Main Page](https://eigen.tuxfamily.org/dox/)
2. [[QuickRef] Dense matrix and array manipulations](https://eigen.tuxfamily.org/dox/group__QuickRefPage.html)
3. [[QuickRef] Sparse linear algebra](https://eigen.tuxfamily.org/dox/group__SparseQuickRefPage.html)
4. [Eigen short ASCII reference](https://eigen.tuxfamily.org/dox/AsciiQuickReference.txt)
5. [zxl19/Eigen-Cheatsheet](https://github.com/zxl19/Eigen-Cheatsheet)
6. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
7. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
8. [qixianyu-buaa/EigenChineseDocument](https://github.com/qixianyu-buaa/EigenChineseDocument)
9. [Aliasing](http://www.eigen.tuxfamily.org/dox/group__TopicAliasing.html)
10. [Catalogue of dense decompositions](https://eigen.tuxfamily.org/dox/group__TopicLinearAlgebraDecompositions.html)
11. [Linear algebra and decompositions](https://eigen.tuxfamily.org/dox/group__TutorialLinearAlgebra.html)
12. [Benchmark of dense decompositions](https://eigen.tuxfamily.org/dox/group__DenseDecompositionBenchmark.html)
13. [Solving linear least squares systems](http://www.eigen.tuxfamily.org/dox/group__LeastSquares.html)
14. [LU分解、LDLT分解和Cholesky分解-CSDN博客](https://blog.csdn.net/zhouliyang1990/article/details/21952485)
15. [奇异值分解（SVD）-漫漫成长的文章-知乎](https://zhuanlan.zhihu.com/p/29846048)
16. [SVD-CSDN博客](https://blog.csdn.net/jiang_he_hu_hai/article/details/78363642)
17. [四元数归一化1-Stack Overflow](https://stackoverflow.com/questions/48019329/difference-between-norm-normalize-and-normalized-in-eigen)
18. [四元数归一化2-CSDN博客](https://blog.csdn.net/m0_56348460/article/details/117386857)
19. [旋转矩阵归一化1-Stack Overflow](https://stackoverflow.com/questions/21761909/eigen-convert-matrix3d-rotation-to-quaternion)
20. [旋转矩阵归一化2-Stack Overflow](https://stackoverflow.com/questions/43896041/eigen-matrix-to-quaternion-and-back-have-different-result)
21. [Alignement issues](https://eigen.tuxfamily.org/dox/group__DenseMatrixManipulation__Alignement.html)
22. [向量化运算-CSDN博客](https://blog.csdn.net/weixin_38251332/article/details/120308863)
23. [Eigen内存对齐1-CSDN博客](https://blog.csdn.net/shyjhyp11/article/details/123208279)
24. [Eigen内存对齐2-CSDN博客](https://blog.csdn.net/shyjhyp11/article/details/123204444)
25. [从Eigen向量化谈内存对齐-王金戈的文章-知乎](https://zhuanlan.zhihu.com/p/93824687)
26. [Eigen内存对齐-卷儿的文章-知乎](https://zhuanlan.zhihu.com/p/349413376)
