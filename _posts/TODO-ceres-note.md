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

```cmake
cmake_minimum_required(VERSION 3.0)
project(project_name)

find_package(Ceres REQUIRED QUIET)

include_directories(
    include
    # ${CERES_INCLUDE_DIRS} # 未设置该变量
)

add_executable(helloworld helloworld.cc)
target_link_libraries(helloworld ${CERES_LIBRARIES})
```

## 最小二乘问题

$$\begin{split}\min_{\mathbf{x}} &\quad \frac{1}{2}\sum_{i} \rho_i\left(\left\|f_i\left(x_{i_1}, ... ,x_{i_k}\right)\right\|^2\right) \\
\text{s.t.} &\quad l_j \le x_j \le u_j\end{split}$$

1. 残差块（ResidualBlock）：$\rho_i\left(\left\|f_i\left(x_{i_1}, ... ,x_{i_k}\right)\right\|^2\right)$；
2. 代价函数（CostFunction）：$f_i(\cdot)$；
3. 参数块（ParameterBlock）：$\left[x_{i_1}, ... ,x_{i_k}\right]$；
4. 损失函数（LossFunction）：$\rho_i(\cdot)$；

## 求导方式

$$\frac{1}{2}(10 -x)^2$$

### 自动求导

```cpp
struct CostFunctor {
  template <typename T>
  bool operator()(const T* const x, T* residual) const {
    residual[0] = 10.0 - x[0];
    return true;
  }
};
```

```cpp
CostFunction* cost_function = new AutoDiffCostFunction<CostFunctor, 1, 1>(new CostFunctor);
problem.AddResidualBlock(cost_function, nullptr, &x);
```

### 解析求导

```cpp
class QuadraticCostFunction : public ceres::SizedCostFunction<1, 1> {
 public:
  bool Evaluate(double const* const* parameters, double* residuals, double** jacobians) const override {
    double x = parameters[0][0];
    residuals[0] = 10 - x;
    if (jacobians != nullptr && jacobians[0] != nullptr) {
      jacobians[0][0] = -1;
    }
    return true;
  }
};
```

```cpp
CostFunction* cost_function = new QuadraticCostFunction;
problem.AddResidualBlock(cost_function, nullptr, &x);
```

### 数值求导

```cpp
struct NumericDiffCostFunctor {
  bool operator()(const double* const x, double* residual) const {
    residual[0] = 10.0 - x[0];
    return true;
  }
};
```

```cpp
cost_function = new NumericDiffCostFunction<NumericDiffCostFunctor, CENTRAL, 1, 1>(new NumericDiffCostFunctor);
problem.AddResidualBlock(cost_function, nullptr, &x);
```

不推荐使用

## 参考

1. [Ceres Solver](http://ceres-solver.org)
