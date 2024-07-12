---
layout: post
title: C++实用程序使用笔记
date: 2022-12-28
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++实用程序使用笔记。

<!-- more -->

## 实用程序

使用时需要包含头文件：

```cpp
#include <utility>
```

### 二元组`pair`

二元关联容器的元素类型是键类型和附加数据类型的组合，这种组合类型可以用一个二元组来表示。

#### 二元组实现

```cpp
template <class T1, class T2>
struct pair {
    T1 first;                                               // 二元组的第一元
    T2 second;                                              // 二元组的第二元
    pair();                                                 // 默认构造函数
    pair(const T1& x, const T2& y);                         // 构造first = x，second = y的二元组
    template <class U, class V> pair(const pair<U, V>& p);  // 拷贝构造函数
    template <class U, class V> pair(pair<U, V>&& p);       // 移动构造函数，&&表示右值引用，C++11引入
    template <class U, class V> pair(U&& x, V&& y);         // 使用右值引用参数，创建pair对象，C++11引入
}
```

### 二元组辅助构造函数`make_pair()`

原型声明：

```cpp
// C++98/03
template <class T1, class T2>
pair<T1, T2> make_pair(T1 x, T2 y);
// C++11
template <class T1, class T2>
pair<V1, V2> make_pair(T1&& x, T2&& y);
```

实现：

```cpp
// C++98/03
template <class T1, class T2>
pair<T1, T2> make_pair(T1 x, T2 y) {
    return (pair<T1, T2>(x, y));
}
// C++11
template <class T1, class T2>
pair<T1, T2> make_pair(T1 x, T2 y) {
    return (pair<V1, V2>(forward<T1>(x), forward<T2>(y)));
}
```

### 完美转发函数`forward()`

原型声明：

```cpp
template <class T>
T&& forward(typename remove_reference<T>::type& arg) noexcept;
template <class T>
T&& forward(typename remove_reference<T>::type&& arg) noexcept;
```

### 强制转换函数`move()`

原型声明：

```cpp
template <class T>
typename remove_reference<T>::type&& move(T&& arg) noexcept;
```

## 参考

1. 《C++语言程序设计》
2. [cplusplus](http://www.cplusplus.com)
3. [cppreference](https://en.cppreference.com/w/)
4. [C++ STL pair用法详解-C语言中文网](http://c.biancheng.net/view/7169.html)
5. [C++11右值引用（一看即懂）-C语言中文网](http://c.biancheng.net/view/7829.html)
6. [C++11完美转发及实现方法详解-C语言中文网](http://c.biancheng.net/view/7868.html)
