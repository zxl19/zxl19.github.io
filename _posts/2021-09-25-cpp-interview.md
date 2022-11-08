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

## C++关键字

### `const`关键字

#### 符号常量

```cpp
const value_type variable_name = variable_value;
```

1. 符号常量在使用之前一定要首先声明：
2. 符号常量不能被赋值：

#### 常对象

```cpp
const class_name object_name;
```

1. 常对象必须进行初始化，而且不能被更新；
2. 在声明常对象时，把`const`关键字放在类型名后面也是允许的，不过人们更习惯于把`const`写在前面；
3. 基本数据类型的常量也可看作一种特殊的常对象，因此，后面将不再对基本数据类型的常量和类类型的常对象加以区分；

#### 用`const`修饰的类成员

##### 常成员函数

```cpp
value_type function_name(variables) const;
```

1. `const`是函数类型的一个组成部分，因此在函数的定义部分也要带`const`关键字；
2. 如果将一个对象声明为常对象，则通过该常对象只能调用它的常成员函数，而不能调用其他成员函数（这就是C++从语法机制上对常对象的保护，也是常对象唯一的对外接口方式）；
3. 无论是否通过常对象调用常成员函数，在常成员函数调用期间，目的对象都被视同为常对象，因此常对象函数不能更新目的对象的数据成员，也不能针对目的对象调用该类中没有用`const`修饰的成员函数（这就保证了在常成员函数中不会更改目的对象的数据成员的值）；
4. `const`关键字可以用于对重载函数的区分，如果仅以`const`关键字为区分对成员函数重载，那么通过非`const`的对象调用该函数，两个重载的函数都可以与之匹配，这时编译器将选择最近的重载函数——不带`const`关键字的函数；

##### 常数据成员

```cpp
const value_type variable_name;
static const value_type variable_name;
```

1. 类的成员数据也可以是常量；
2. 常数据成员只能通过初始化列表来获得初值；
3. 静态常数据成员在类外说明和初始化；

#### 常引用

```cpp
const value_type &reference_name;
```

1. 常引用所引用的对象不能被更新；
2. 如果用常引用作形参，便不会意外地发生对实参的更改；
3. 对于在函数中无须改变其值的参数，不宜使用普通引用方式传递，因为那会使得常对象无法被传入，采用传值方式或传递常引用的方式可避免这一问题；
4. 对于大对象来说，传值耗时较多，因此传递常引用为宜；
5. 复制构造函数的参数一般也宜采用常引用传递；

### `delete`关键字

### `enum`关键字

### `extern`关键字

### `friend`关键字

### `inline`关键字

```cpp
inline value_type function_name(variables) {
    // implementation
}
```

1. 内联函数不是在调用时发生控制转移，而是在编译时将函数体嵌入在每一个调用处；
2. 对于一些功能简单、规模较小又使用频繁的函数，可以设计为内联函数；

### `override`关键字

### `static`关键字

#### 静态数据成员

1. 如果某个属性为整个类所共有，不属于任何一个具体对象，则采用`static`关键字来声明为静态成员；
2. 类属性是描述类的所有对象共有特征的一个数据项，对于任何对象实例，它的属性值是相同的；
3. 静态数据成员具有静态生存期；
4. 由于静态数据成员不属于任何一个对象，因此可以通过类名对它进行访问，一般的用法是`类名::标识符`；

#### 静态函数成员

```cpp
static value_type function_name(variables);
```

1. 静态成员函数可以直接访问该类的静态数据和函数成员；
2. 而访问非静态成员，必须通过对象名；

### `this`关键字

### `typedef`关键字

### `union`关键字

### 关于`static`

### 关于`this`

### `using`关键字

### `virtual`关键字

#### 虚函数

虚函数是动态绑定的基础。虚函数必须是非静态的成员函数。虚函数经过派生之后，在类族中就可以实现运行过程中的多态。

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

### 结构体`struct`和共用体`union`

### `#define`和`const`

### `const`和`constexpr`

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

### 关于嵌套模板中相邻的右尖括号

C++11支持嵌套模板中相邻的右尖括号写作`>>`：

```cpp
vector<vector<int>>
```

早期C++标准要求嵌套模板中相邻的右尖括号写作`> >`：

```cpp
vector<vector<int> >
```

其原因是为了避免与输入流运算符`>>`混淆，否则会报错：

```text
`>>' should be `> >' within a nested template argument list.
```

### 关于`auto`和`decltype`

1. `auto`：让编译器在编译器就推导出变量的类型，可以通过`=`右边的类型推导出变量的类型；
2. `decltype`：相对于`auto`用于推导变量类型，而`decltype`则用于推导表达式类型，这里只用于编译器分析表达式的类型，表达式实际不会进行运算；

### `constexpr`关键字

### `default`关键字

### `for`循环

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
9. [嵌套模板中的>>1-Stack Overflow](https://stackoverflow.com/questions/6695261/template-within-template-why-should-be-within-a-nested-template-arg)
10. [嵌套模板中的>>2-Stack Overflow](https://stackoverflow.com/questions/7087033/for-nested-templates-when-did-become-standard-c-instead-of)
11. [C++11新特性，所有知识点都在这了！-程序喵大人的文章-知乎](https://zhuanlan.zhihu.com/p/139515439)
12. [C++智能指针-小小将的文章-知乎](https://zhuanlan.zhihu.com/p/54078587)
