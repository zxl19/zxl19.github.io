---
layout: post
title: C++数学常数使用笔记
date: 2024-04-06
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++数学常数使用笔记。

<!-- more -->

## 数学常数

### 使用模板类

1. C++20引入，使用时需要包含头文件：

    ```cpp
    #include <numbers>
    ```

2. 定义的数学常数均在`numbers`子命名空间中，为了使表示形式简便，本文默认使用`std::numbers`命名空间：

    ```cpp
    using namespace std::numbers;
    ```

3. 原型声明：

    ```cpp
    namespace std::numbers {
    template <class T>
    inline constexpr T e_v = /* unspecified */;
    template <class T>
    inline constexpr T log2e_v = /* unspecified */;
    template <class T>
    inline constexpr T log10e_v = /* unspecified */;
    template <class T>
    inline constexpr T pi_v = /* unspecified */;
    template <class T>
    inline constexpr T inv_pi_v = /* unspecified */;
    template <class T>
    inline constexpr T inv_sqrtpi_v = /* unspecified */;
    template <class T>
    inline constexpr T ln2_v = /* unspecified */;
    template <class T>
    inline constexpr T ln10_v = /* unspecified */;
    template <class T>
    inline constexpr T sqrt2_v = /* unspecified */;
    template <class T>
    inline constexpr T sqrt3_v = /* unspecified */;
    template <class T>
    inline constexpr T inv_sqrt3_v = /* unspecified */;
    template <class T>
    inline constexpr T egamma_v = /* unspecified */;
    template <class T>
    inline constexpr T phi_v = /* unspecified */;

    template <floating_point T>
    inline constexpr T e_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T log2e_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T log10e_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T pi_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T inv_pi_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T inv_sqrtpi_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T ln2_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T ln10_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T sqrt2_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T sqrt3_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T inv_sqrt3_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T egamma_v<T> = /* see description */;
    template <floating_point T>
    inline constexpr T phi_v<T> = /* see description */;

    inline constexpr double e = e_v<double>;
    inline constexpr double log2e = log2e_v<double>;
    inline constexpr double log10e = log10e_v<double>;
    inline constexpr double pi = pi_v<double>;
    inline constexpr double inv_pi = inv_pi_v<double>;
    inline constexpr double inv_sqrtpi = inv_sqrtpi_v<double>;
    inline constexpr double ln2 = ln2_v<double>;
    inline constexpr double ln10 = ln10_v<double>;
    inline constexpr double sqrt2 = sqrt2_v<double>;
    inline constexpr double sqrt3 = sqrt3_v<double>;
    inline constexpr double inv_sqrt3 = inv_sqrt3_v<double>;
    inline constexpr double egamma = egamma_v<double>;
    inline constexpr double phi = phi_v<double>;
    }  // namespace std::numbers
    ```

### 使用宏定义

1. 使用时需要包含头文件：

    ```cpp
    #include <cmath>
    ```

2. 原型声明：

    ```cpp
    #if defined __USE_MISC || defined __USE_XOPEN
    #define M_E 2.7182818284590452354         /* e */
    #define M_LOG2E 1.4426950408889634074     /* log_2 e */
    #define M_LOG10E 0.43429448190325182765   /* log_10 e */
    #define M_LN2 0.69314718055994530942      /* log_e 2 */
    #define M_LN10 2.30258509299404568402     /* log_e 10 */
    #define M_PI 3.14159265358979323846       /* pi */
    #define M_PI_2 1.57079632679489661923     /* pi/2 */
    #define M_PI_4 0.78539816339744830962     /* pi/4 */
    #define M_1_PI 0.31830988618379067154     /* 1/pi */
    #define M_2_PI 0.63661977236758134308     /* 2/pi */
    #define M_2_SQRTPI 1.12837916709551257390 /* 2/sqrt(pi) */
    #define M_SQRT2 1.41421356237309504880    /* sqrt(2) */
    #define M_SQRT1_2 0.70710678118654752440  /* 1/sqrt(2) */
    #endif
    ```

## 参考

1. [cppreference](https://en.cppreference.com/w/)
2. [Math Constants-Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-runtime-library/math-constants?view=msvc-170)
