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

1. Sophus是基于Eigen实现的李群和李代数库；
2. Sophus是纯头文件库，使用时需要包含头文件：

    ```cpp
    #include "sophus/so3.hpp"       // SO(3)李群
    #include "sophus/se3.hpp"       // SE(3)李群
    ```

3. Sophus官方并没有提供安装和使用教程，以下内容主要整理自《视觉SLAM十四讲》；

## CMakeLists

```cmake
# 方法一：本地安装
find_package(Sophus REQUIRED QUIET)
# 方法二：非本地安装
set(SOPHUS_INCLUDE_DIRS "${PROJECT_SOURCE_DIR}/third_party/Sophus")

include_directories(${SOPHUS_INCLUDE_DIRS})
```

## SO(3)李群

```cpp
Eigen::Matrix3d R;
Eigen::Quaterniond q(R);
Sophus::SO3d SO3(R);                            // 通过旋转矩阵构造Sophus::SO3d
Sophus::SO3d SO3(q);                            // 通过四元数构造Sophus::SO3d
Sophus::SO3d SO3_inv = SO3.inverse();           // 取李群逆
Eigen::Matrix3d R = SO3.matrix();               // 取旋转矩阵
Eigen::Quaterniond q = SO3.unit_quaternion();   // 取单位四元数

// 提取围绕固定坐标轴的旋转角，单位为弧度
// 符合外旋欧拉角的定义，常用于组合导航设备
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

```cpp
Eigen::Matrix3d R;
Eigen::Quaterniond q(R);
Eigen::Vector3d t(1, 0, 0);
Sophus::SE3d SE3(R, t);                         // 通过R，t构造Sophus::SE3d
Sophus::SE3d SE3(q, t);                         // 通过q，t构造Sophus::SE3d
Sophus::SE3d SE3_inv = SE3.inverse();           // 取李群逆
Sophus::SO3d SO3 = SE3.so3();                   // 取SO(3)李群
Eigen::Matrix4d T = SE3.matrix();               // 取变换矩阵
Eigen::Matrix3d R = SE3.so3().matrix();         // 取旋转矩阵
Eigen::Quaterniond q = SE3.unit_quaternion();   // 取单位四元数，本质上是调用this->so3().unit_quaternion()
Eigen::Vector3d t = SE3.translation();          // 取平移向量

// 取欧拉角，单位为弧度
double euler_x = SE3.angleX();                  // 围绕x轴旋转的欧拉角，即滚转角（roll），本质上是调用this->so3().angleX()
double euler_y = SE3.angleY();                  // 围绕y轴旋转的欧拉角，即俯仰角（pitch），本质上是调用this->so3().angleY()
double euler_z = SE3.angleZ();                  // 围绕z轴旋转的欧拉角，即偏航角（yaw），本质上是调用this->so3().angleZ()

// 通过欧拉角构造Sophus::SE3d的旋转部分，旋转顺序为ZYX，单位为弧度
SE3.so3() = SO3d::rotX(euler_x) * SO3d::rotY(euler_y) * SO3d::rotZ(euler_z);

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
2. [CMakeLists添加Sophus库-CSDN博客](https://blog.csdn.net/weixin_38213410/article/details/98114423)
3. [Sophus库的安装和使用教程-CSDN博客](https://blog.csdn.net/u011092188/article/details/77833022)
4. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
5. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
