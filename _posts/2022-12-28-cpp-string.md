---
layout: post
title: C++字符串类使用笔记
date: 2022-12-28
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++字符串类使用笔记。

<!-- more -->

## 字符串类

1. C++可以使用字符数组表示字符串，存在诸多不便：

    ```cpp
    // 将字符串常量赋值给指向常量的指针
    const char* str = "program";
    // 将字符串变量赋值给字符数组
    char str1[8] = {'p', 'r', 'o', 'g', 'r', 'a', 'm', '\0'};
    char str2[8] = "program";
    char str3[] = "program";
    ```

    - 字符串操作需要使用`<cstring>`头文件中定义的字符串处理函数；
    - 当字符串长度不确定时，需要手动进行动态内存分配；

2. C++将字符串相关操作进行了封装，形成了字符串类`string`；
3. 严格来说，`string`是类模板`basic_string`的一个特化实例，但是其使用时的特点与类相同，可以当做一个类来使用；
4. 字符串类不是标准模板类（Standard Template Library，STL）的一部分；
5. 使用时需要包含头文件：

    ```cpp
    #include <string>
    ```

### 操作符

| 操作符 | 示例 | 含义 |
| :---- | :---- | :----|
| + | `s + t` | 将串`s`和`t`连接成一个新串 |
| = | `s = t` | 用`t`更新`s` |
| += | `s += t` | 等价于`s = s + t` |
| == | `s == t` | 判断`s`与`t`是否相等 |
| != | `s != t` | 判断`s`与`t`是否不等 |
| < | `s < t` | 判断`s`是否小于`t` |
| <= | `s <= t` | 判断`s`是否小于或等于`t` |
| > | `s > t` | 判断`s`是否大于`t` |
| >= | `s >= t` | 判断`s`是否大于或等于`t` |
| [] | `s[i]` | 访问串中下标为`i`的字符，也可通过成员函数`s.at(i)` |

### 常用基本功能

```cpp
size_t s.size()
bool s.empty()
void s.push_back(char c)                        // 追加单个字符
void s.pop_back()
string s.substr(size_t pos, size_t len)         // 取子字符串
void s.append(const string& str)                // 追加字符串
```

### 遍历字符串

```cpp
for (size_t i = 0; i < s.size(); i++)           // 常规方式
for (char c : s)                                // C++11引入
for (char& c : s)                               // C++11引入，速度更快
```

## 参考

1. 《C++语言程序设计》
2. [cplusplus](http://www.cplusplus.com)
3. [字符串1-CSDN博客](https://blog.csdn.net/qq_38537503/article/details/106279850)
4. [字符串2-CSDN博客](https://blog.csdn.net/qq_42270373/article/details/84589231)
5. [字符串3-CSDN博客](https://blog.csdn.net/weixin_36670529/article/details/108401528)
