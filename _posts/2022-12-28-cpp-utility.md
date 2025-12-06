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

#### 二元组辅助构造函数`make_pair()`

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

### 右值引用`&&`

1. 左值（locator value，lvalue）是存储在内存中，有明确存储地址的数据，可寻址；
2. 右值（read value，rvalue）是可以提供数据值的数据，不一定可以寻址，例如存储于寄存器中的数据；
3. 判断依据：

    - 可位于赋值符号左侧的表达式是左值，反之，只能位于赋值符号右侧的表达式是右值；
    - 有名称的，可以获取到存储地址的表达式是左值，反之，为右值；

4. `&`称为左值引用，只能操作左值，无法操作右值，允许使用常量左值引用操作右值；
5. `&&`称为右值引用，C++11引入，以引用传递而非值传递的方式使用右值，主要用于移动语义和完美转发；
6. 右值引用必须立即进行初始化，且只能使用右值进行初始化；
7. 右值引用可以对于右值进行修改，也支持常量右值引用，但是无实际用途；

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

1. 编译器会进行拷贝省略（copy elision）优化，直接在目标位置处构造返回值，避免拷贝构造和移动构造：

    - 返回值优化（Return Value Optimization，RVO）：函数返回临时对象（通常是由构造函数直接初始化的匿名对象）；
    - 具名返回值优化（Named Return Value Optimization，NRVO）：函数返回已命名的局部对象；

2. 以上两种情况不需要使用`move()`，否则会影响性能：

## 参考

1. 《C++语言程序设计》
2. [cplusplus](http://www.cplusplus.com)
3. [cppreference](https://en.cppreference.com/w/)
4. [C++ STL pair用法详解-C语言中文网](https://c.biancheng.net/view/7169.html)
5. [请问auto&&中的两个&&啥意思?-rayhunter的回答-知乎](https://www.zhihu.com/question/325315863/answer/2685468097)
6. [C++11右值引用-C语言中文网](https://c.biancheng.net/view/7829.html)
7. [C++11右值引用详解-C语言中文网](https://c.biancheng.net/view/439.html)
8. [C++中的右值引用-C语言中文网](https://c.biancheng.net/view/cte7w1y.html)
9. [C++11完美转发及实现方法详解-C语言中文网](https://c.biancheng.net/view/7868.html)
10. [聊聊C++中的完美转发-李超的文章-知乎](https://zhuanlan.zhihu.com/p/161039484)
11. [C++11 move()函数：将左值强制转换为右值-C语言中文网](https://c.biancheng.net/view/7863.html)
12. [一文读懂C++右值引用和std::move-腾讯技术工程的文章-知乎](https://zhuanlan.zhihu.com/p/335994370)
13. [C++的移动语义究竟是怎么实现的？-南山烟雨珠江潮的回答-知乎](https://www.zhihu.com/question/659439772/answer/1980590424755298862)
14. [C++函数返回局部变量的std::move()问题？-神奇先生的回答-知乎](https://www.zhihu.com/question/57048704/answer/151446405)
15. [深入浅出RVO、NRVO以及std::move的策略与影响-未平的文章-知乎](https://zhuanlan.zhihu.com/p/665538550)
16. [每个C++工程师都要了解的十个性能陷阱-尚晋的文章-知乎](https://zhuanlan.zhihu.com/p/569174076)
