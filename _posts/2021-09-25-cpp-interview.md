---
layout: post
title: C++面试知识点总结
date: 2021-09-25
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

C++面试知识点总结。

<!-- more -->

**整理中**

## C++ Hello World

### C++和C的区别

1. **C++是面向对象的语言，C是面向过程的语言；**
2. C++引入`new/delete`运算符，取代了C中的`malloc/free`库函数；
3. C++引入引用的概念，而C中没有；
4. C++引入类的概念，而C中没有；
5. C++引入函数重载的特性，而C中没有；

### 面向对象的三大特征

1. **封装**：封装是面向对象方法的一个重要原则，就是把对象的属性和服务结合成一个独立的系统单位，并尽可能隐蔽对象的内部细节；
2. **继承**：特殊类的对象用于其一般类的全部属性与服务，称作特殊类对一般类的继承；
3. **多态**：多态性是指在一般类中定义的属性或行为，被特殊类继承之后，可以具有不同的数据类型或表现出不同的行为；

    - 静态多态：编译时的多态，绑定工作在编译连接阶段完成，称为静态绑定，e.g. 函数重载（包括运算符重载）；
    - 动态多态：运行时的多态，绑定工作在程序运行阶段完成，称为动态绑定，e.g. 虚函数；

## 关键字用法

### 关于`const`

### 关于`delete`

### 关于`enum`

### 关于`extern`

### 关于`friend`

### 关于`inline`

### 关于`static`

### 关于`this`

### 关于`typedef`

### 关于`virtual`

#### 虚函数

##### 一般虚函数成员

```cpp
virtual value_type function_name(variables);
```

1. 虚函数声明只能出现在类定义中的函数原型声明中，而不能在成员函数实现的时候；
2. 运行过程中的多态需要满足三个条件：

    - 赋值兼容原则；
    - 虚函数；
    - 由成员函数来调用或者是通过指针、引用来访问虚函数；

3. 虚函数一般不声明为内联函数，因为对虚函数的调用需要动态绑定，而对内联函数的处理是静态的，所以虚函数一般不能以内联函数处理。但将虚函数声明为内联函数也不会引起错误；

##### 虚析构函数

```cpp
virtual ~ClassName();
```

#### 纯虚函数和抽象类

##### 纯虚函数

```cpp
virtual value_type function_name(variables) = 0;
```

##### 抽象类

1. 带有纯虚函数的类是抽象类；
2. 抽象类不能实例化；

## 区别辨析

### 结构体`struct`和类`class`

### `#define`和`const`

### `size_t`和`int`

```cpp
typedef unsigned int size_t;    // 32位
typedef unsigned long size_t;   // 64位
```

与`int`固定四个字节不同，`size_t`的取值范围是目标平台下最大可能的数组尺寸，一些平台下`size_t`的范围小于`int`的正数范围，又或者大于`unsigned int`，使用`int`既有可能浪费，又有可能范围不够大。

### `NULL`和`nullptr`

为解决`NULL`代指空指针存在的二义性问题，在C++11中引入`nullptr`关键字来代指空指针：

```cpp
NULL        // 0
nullptr     // 空指针，C++11引入
```

## C++11

### 关于模板嵌套中的`>>`

C++11要求嵌套模板类右侧的尖括号分开，为了避免与输入流运算符`>>`混淆：

```cpp
vector<vector<int> >
```

否则会报错：

```text
`>>' should be `> >' within a nested template argument list
```

### 关于`auto`和`decltype`

1. `auto`：让编译器在编译器就推导出变量的类型，可以通过=右边的类型推导出变量的类型；
2. `decltype`：相对于`auto`用于推导变量类型，而`decltype`则用于推导表达式类型，这里只用于编译器分析表达式的类型，表达式实际不会进行运算；

### 关于`default`

### 关于`for`

基于范围的`for`循环：

```cpp
vector<int> vec;
for (int i : vec) {}
string str;
for (char c : str) {}
```

### 关于智能指针

1. `std::shared_ptr`
2. `std::weak_ptr`
3. `std::unique_ptr`
4. `std::auto_ptr`：C++11弃用，C++17移出；

## 参考

1. 《C++语言程序设计》
2. [校招C++大概学习到什么程度？-程序员内功修炼的回答-知乎](https://www.zhihu.com/question/290102232/answer/2094675219)
3. [C++教程-菜鸟教程](https://www.runoob.com/cplusplus/cpp-tutorial.html)
4. [C++入门教程-C语言中文网](http://c.biancheng.net/cplus/)
5. [C++11教程-C语言中文网](http://c.biancheng.net/cplus/11/)
6. [siez_t和int1-CSDN博客](https://blog.csdn.net/wc11223/article/details/70553583)
7. [siez_t和int2-CSDN博客](https://blog.csdn.net/qq_41598072/article/details/84924997)
8. [NULL和nullptr-CSDN博客](https://blog.csdn.net/qq_18108083/article/details/84346655)
9. [模板嵌套中的>>-Stack Overflow](https://stackoverflow.com/questions/6695261/template-within-template-why-should-be-within-a-nested-template-arg)
10. [C++11新特性，所有知识点都在这了！-程序喵大人的文章-知乎](https://zhuanlan.zhihu.com/p/139515439)
11. [C++智能指针-小小将的文章-知乎](https://zhuanlan.zhihu.com/p/54078587)
