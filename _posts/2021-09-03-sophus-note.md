---
layout: post
title: Sophus库使用笔记
date: 2021-09-03
author: zxl19
tags: [C++, Sophus, Note]
comments: true
toc: true
pinned: false
---

我的Sophus库使用笔记。

<!-- more -->

## Sophus Hello World

1. Sophus是基于Eigen实现的李群（Lie group）和李代数（Lie algebra）[^1]库；
2. Sophus是纯头文件库，使用时需要包含头文件：

    ```cpp
    #include "sophus/so3.hpp"       // SO(3)李群
    #include "sophus/se3.hpp"       // SE(3)李群
    ```

3. Sophus官方并没有提供安装和使用教程，以下内容主要整理自《视觉SLAM十四讲》；

[^1]: 以这一概念的提出者，挪威数学家Sophus Lie的名字命名。

## CMakeLists

```cmake
# 方法一：本地安装（待测试）
find_package(Sophus REQUIRED QUIET)
# 方法二：非本地安装（推荐）
set(SOPHUS_INCLUDE_DIRS "${PROJECT_SOURCE_DIR}/third_party/Sophus")

include_directories(${SOPHUS_INCLUDE_DIRS})
```

## SO(3)李群

$\mathrm{SO}\left(3\right)$李群定义：

$$\mathrm{SO}\left(3\right) = \left\{\left.\boldsymbol{R}\in\mathrm{GL}\left(3\right)\right|\boldsymbol{RR}^{\mathrm{T}}, \mathrm{det}\left(\boldsymbol{R}\right) = 1\right\}$$

$\mathfrak{so}\left(3\right)$李代数定义：

$$\mathfrak{so}\left(3\right) = \left\{\boldsymbol{\phi}\in\mathbb{R}^{3}, \boldsymbol{\Phi} = \boldsymbol{\phi}^{\wedge}\in\mathbb{R}^{3\times 3}\right\}$$

```cpp
Eigen::Matrix3d R;                              // 要求旋转矩阵满足SO(3)李群的定义
Eigen::Quaterniond q(R);                        // 要求四元数的模长不能接近0
// 通过旋转矩阵构造Sophus::SO3d
Sophus::SO3d SO3(R);
// 通过四元数构造Sophus::SO3d
Sophus::SO3d SO3(q);
SO3.setQuaternion(q);                           // 会隐式将四元数归一化

Sophus::SO3d SO3_inv = SO3.inverse();           // 取李群逆
Eigen::Matrix3d R = SO3.matrix();               // 取旋转矩阵
Eigen::Quaterniond q = SO3.unit_quaternion();   // 取单位四元数

// 提取围绕固定坐标轴的旋转角，单位为弧度
double euler_x = SO3.angleX();                  // 围绕x轴的旋转角
double euler_y = SO3.angleY();                  // 围绕y轴的旋转角
double euler_z = SO3.angleZ();                  // 围绕z轴的旋转角

// 通过欧拉角构造Sophus::SO3d，旋转顺序为ZYX，单位为弧度
// 内旋欧拉角，右乘
SO3 = SO3d::rotZ(yaw_rad) * SO3d::rotY(pitch_rad) * SO3d::rotX(roll_rad);
// 外旋欧拉角，左乘
SO3 = SO3d::rotX(roll_rad) * SO3d::rotY(pitch_rad) * SO3d::rotZ(yaw_rad);

// 使用对数映射获得李代数
Eigen::Vector3d so3 = SO3.log();
// hat为向量到反对称矩阵
Sophus::SO3d::hat(so3)
// vee为反对称矩阵到向量
Sophus::SO3d::vee(Sophus::SO3d::hat(so3))

// 增量扰动模型的更新
Eigen::Vector3d update_so3(1e-4, 0, 0);         // 更新量
Sophus::SO3d SO3_updated = Sophus::SO3d::exp(update_so3) * SO3;
```

## SE(3)李群

$\mathrm{SE}\left(3\right)$李群定义：

$$\mathrm{SE}\left(3\right) = \left\{\left.\boldsymbol{T} =
\begin{bmatrix}
    \boldsymbol{R} & \boldsymbol{t} \\
    \boldsymbol{0}^{\mathrm{T}} & 1
\end{bmatrix}
\in\mathrm{GL}\left(4\right)\right|\boldsymbol{R}\in\mathrm{SO}\left(3\right), \boldsymbol{t}\in\mathbb{R}^{3}\right\}$$

$\mathfrak{se}\left(3\right)$李代数定义：

$$\mathfrak{se}\left(3\right) = \left\{\left.\boldsymbol{\xi} =
\begin{bmatrix}
    \boldsymbol{\rho} \\
    \boldsymbol{\phi}
\end{bmatrix}\in\mathbb{R}^{6}\right|\boldsymbol{\rho}\in\mathbb{R}^{3}, \boldsymbol{\phi}\in\mathfrak{so}\left(3\right), \boldsymbol{\xi}^{\wedge} =
\begin{bmatrix}
    \boldsymbol{\phi}^{\wedge} & \boldsymbol{\rho} \\
    \boldsymbol{0}^{\mathrm{T}} & 0
\end{bmatrix}\in\mathbb{R}^{4\times 4}\right\}$$

```cpp
Eigen::Matrix3d R;                              // 要求旋转矩阵满足SO(3)李群的定义
Eigen::Quaterniond q(R);                        // 要求四元数的模长不能接近0
Eigen::Vector3d t(1, 0, 0);
// 通过旋转矩阵和平移向量构造Sophus::SE3d
Sophus::SE3d SE3(R, t);
SE3.setRotationMatrix(R);                       // 先将旋转矩阵转为四元数，本质上是调用this->so3().setQuaternion()
SE3.translation() = t;
// 通过四元数和平移向量构造Sophus::SE3d
Sophus::SE3d SE3(q, t);
SE3.setQuaternion(q);                           // 本质上是调用this->so3().setQuaternion()
SE3.translation() = t;

Sophus::SE3d SE3_inv = SE3.inverse();           // 取李群逆
Sophus::SO3d SO3 = SE3.so3();                   // 取SO(3)李群
Eigen::Matrix4d T = SE3.matrix();               // 取变换矩阵
Eigen::Matrix3d R = SE3.so3().matrix();         // 取旋转矩阵
Eigen::Quaterniond q = SE3.unit_quaternion();   // 取单位四元数，本质上是调用this->so3().unit_quaternion()
Eigen::Vector3d t = SE3.translation();          // 取平移向量

// 提取围绕固定坐标轴的旋转角，单位为弧度
// 符合外旋欧拉角的定义，常用于组合导航设备
double euler_x = SE3.angleX();                  // 围绕x轴的旋转角，本质上是调用this->so3().angleX()
double euler_y = SE3.angleY();                  // 围绕y轴的旋转角，本质上是调用this->so3().angleY()
double euler_z = SE3.angleZ();                  // 围绕z轴的旋转角，本质上是调用this->so3().angleZ()

// 通过欧拉角构造Sophus::SE3d的旋转部分，旋转顺序为ZYX，单位为弧度
// so3()成员函数定义了返回引用和返回常引用两个版本，在调用时可以作为等号左值和等号右值使用
// 内旋欧拉角，右乘
SE3.so3() = SO3d::rotZ(yaw_rad) * SO3d::rotY(pitch_rad) * SO3d::rotX(roll_rad);
// 外旋欧拉角，左乘
SE3.so3() = SO3d::rotX(roll_rad) * SO3d::rotY(pitch_rad) * SO3d::rotZ(yaw_rad);

// 通过欧拉角构造只包含旋转部分的Sophus::SE3d，旋转顺序为ZYX，单位为弧度
// 内旋欧拉角，右乘
SE3 = SE3d::rotZ(yaw_rad) * SE3d::rotY(pitch_rad) * SE3d::rotX(roll_rad);
// 外旋欧拉角，左乘
SE3 = SE3d::rotX(roll_rad) * SE3d::rotY(pitch_rad) * SE3d::rotZ(yaw_rad);

// 通过平移向量构造只包含平移部分的Sophus::SE3d，平移顺序不限
// translation()成员函数定义了返回引用和返回常引用两个版本，在调用时可以作为等号左值和等号右值使用
SE3.translation() = t;
SE3.trans(x, y, z);
SE3 = SE3d::transX(x) * SE3d::transY(y) * SE3d::transZ(z);

// 李代数se(3)是一个六维向量，方便起见先typedef一下
typedef Eigen::Matrix<double, 6, 1> Vector6d;
// 使用对数映射获得李代数，在Sophus中，se(3)的平移在前，旋转在后
Vector6d se3 = SE3_Rt.log();
// hat为向量到反对称矩阵
Sophus::SE3d::hat(se3)
// vee为反对称矩阵到向量
Sophus::SE3d::vee(Sophus::SE3d::hat(se3))

// 增量扰动模型的更新
Vector6d update_se3;                            // 更新量
update_se3.setZero();
update_se3(0, 0) = 1e-4;
Sophus::SE3d SE3_updated = Sophus::SE3d::exp(update_se3) * SE3_Rt;
```

## 参考

1. [strasdat/Sophus](https://github.com/strasdat/Sophus)
2. [Sophus Lie-Britannica](https://www.britannica.com/biography/Sophus-Lie)
3. [Sophus Lie-MacTutor](https://mathshistory.st-andrews.ac.uk/Biographies/Lie/)
4. [CMakeLists添加Sophus库-CSDN博客](https://blog.csdn.net/weixin_38213410/article/details/98114423)
5. [Sophus库的安装和使用教程-CSDN博客](https://blog.csdn.net/u011092188/article/details/77833022)
6. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
7. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
