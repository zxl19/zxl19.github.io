---
layout: post
title: C++数值极限类使用笔记
date: 2024-04-06
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++数值极限类使用笔记。

<!-- more -->

## 数值极限类

1. `std::numeric_limits`模板类用于提供编译平台上的算数类型信息；
2. 使用时需要包含头文件：

    ```cpp
    #include <limits>
    ```

3. `std::numeric_limits`模板类对于基本算数类型（fundamental arithmetic types）进行了特化（specialize），基本算数类型包括整型（bool、char、int等）和浮点型（float、double等）：
4. 原型声明：

    ```cpp
    template <class T>
    class numeric_limits {
    public:
      static constexpr bool is_specialized = false;
      static constexpr T min() noexcept { return T(); }
      static constexpr T max() noexcept { return T(); }
      static constexpr T lowest() noexcept { return T(); }
      static constexpr int digits = 0;
      static constexpr int digits10 = 0;
      static constexpr bool is_signed = false;
      static constexpr bool is_integer = false;
      static constexpr bool is_exact = false;
      static constexpr int radix = 0;
      static constexpr T epsilon() noexcept { return T(); }
      static constexpr T round_error() noexcept { return T(); }

      static constexpr int min_exponent = 0;
      static constexpr int min_exponent10 = 0;
      static constexpr int max_exponent = 0;
      static constexpr int max_exponent10 = 0;

      static constexpr bool has_infinity = false;
      static constexpr bool has_quiet_NaN = false;
      static constexpr bool has_signaling_NaN = false;
      static constexpr float_denorm_style has_denorm = denorm_absent;
      static constexpr bool has_denorm_loss = false;
      static constexpr T infinity() noexcept { return T(); }
      static constexpr T quiet_NaN() noexcept { return T(); }
      static constexpr T signaling_NaN() noexcept { return T(); }
      static constexpr T denorm_min() noexcept { return T(); }

      static constexpr bool is_iec559 = false;
      static constexpr bool is_bounded = false;
      static constexpr bool is_modulo = false;

      static constexpr bool traps = false;
      static constexpr bool tinyness_before = false;
      static constexpr float_round_style round_style = round_toward_zero;
    };
    ```

## 参考

1. [cplusplus](https://cplusplus.com)
