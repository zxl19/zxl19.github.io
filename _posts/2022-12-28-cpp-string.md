---
layout: post
title: C++字符串使用笔记
date: 2022-12-28
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++字符串使用笔记。

<!-- more -->

## 字符串`string`

使用时需要包含头文件：

```cpp
#include <string>
```

### 操作符

| 操作符 | 示例 | 含义 |
| :---- | :---- | :----|
| + | `s + t` | 将串`s`和`t`连接成一个新串 |
| = | `s = t` | 用t更新s |
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
