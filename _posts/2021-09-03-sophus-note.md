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

## Hello World

1. Sophus是基于Eigen实现的李群和李代数库；
2. 使用中需包含如下头文件：

    ```cpp
    #include "sophus/so3.hpp"
    #include "sophus/se3.hpp"
    ```

## SO(3)位姿表示

```cpp
Quaterniond q(R);
Sophus::SO3d SO3_R(R);  // Sophus::SO3d可以直接从旋转矩阵构造
Sophus::SO3d SO3_q(q);  // 也可以通过四元数构造，二者是等价的
SO3_R.matrix()          // 转成矩阵
SO3_q.matrix()          // 转成矩阵

// 使用对数映射获得它的李代数
Vector3d so3 = SO3_R.log();
// hat 为向量到反对称矩阵
Sophus::SO3d::hat(so3)
// 相对的，vee为反对称到向量
Sophus::SO3d::vee(Sophus::SO3d::hat(so3)).transpose()

// 增量扰动模型的更新
Vector3d update_so3(1e-4, 0, 0);    // 更新量
Sophus::SO3d SO3_updated = Sophus::SO3d::exp(update_so3) * SO3_R;
```

## SE(3)位姿表示

```cpp
// 对SE(3)操作大同小异
Vector3d t(1, 0, 0);            // 沿X轴平移1
Sophus::SE3d SE3_Rt(R, t);      // 从R,t构造SE(3)
Sophus::SE3d SE3_qt(q, t);      // 从q,t构造SE(3)
SE3_Rt.matrix()
SE3_qt.matrix()
// 李代数se(3) 是一个六维向量，方便起见先typedef一下
typedef Eigen::Matrix<double, 6, 1> Vector6d;
Vector6d se3 = SE3_Rt.log();
// 观察输出，会发现在Sophus中，se(3)的平移在前，旋转在后.
// 同样的，有hat和vee两个算符
Sophus::SE3d::hat(se3)
Sophus::SE3d::vee(Sophus::SE3d::hat(se3)).transpose()

// 最后，演示一下更新
Vector6d update_se3;    // 更新量
update_se3.setZero();
update_se3(0, 0) = 1e-4;
Sophus::SE3d SE3_updated = Sophus::SE3d::exp(update_se3) * SE3_Rt;
```

## 参考

1. [strasdat/Sophus](https://github.com/strasdat/Sophus)
2. [Sophus库的安装和使用教程-CSDN博客](https://blog.csdn.net/u011092188/article/details/77833022)
3. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
4. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
