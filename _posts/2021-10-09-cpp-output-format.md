---
layout: post
title: C++设置输出样式
date: 2021-10-09
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

C++设置输出样式的方法，包括输出到文件和终端中的数字格式、字体和底纹样式。

<!-- more -->

## 文件输出

```cpp
#include <iostream>

int main() {
    std::ofstream outfile("output.txt", std::ios::out);
    outfile << "Hello World!" << std::endl;
    return 0;
}
```

## 数字格式

### 有效数字和小数位数

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double pi = 3.14159265;

    // 输出六位有效数字：3.14159
    std::cout << std::setprecision(6) << pi << std::endl;

    // 固定小数点，输出六位小数：3.141593
    // 全局设置
    std::cout.setf(std::ios::fixed);
    std::cout << std::setprecision(6) << pi << std::endl;
    std::cout.unsetf(std::ios::fixed);
    // 局部设置
    std::cout << std::ios::fixed << std::setprecision(6) << pi << std::endl;
    return 0;
}
```

## 文字和底纹样式

### 使用ANSI转义序列

#### 复杂实现

使用带参数宏定义了字体和底纹样式：

```cpp
//
// colors.hpp
//
// Posted by Gon1332 May 15 2015 on StackOverflow
// https://stackoverflow.com/questions/2616906/how-do-i-output-coloured-text-to-a-linux-terminal#2616912
//
// Description: An easy header file to make colored text output to terminal second nature.
// Modified by Shades Aug. 14 2018

// PLEASE carefully read comments before using this tool, this will save you a lot of bugs that are going to be just about impossible to find.
#ifndef COLORS_HPP
#define COLORS_HPP

/* FOREGROUND */
// These codes set the actual text to the specified color
#define RESETTEXT "\x1B[0m"  // Set all colors back to normal.
#define FOREBLK   "\x1B[30m" // Black
#define FORERED   "\x1B[31m" // Red
#define FOREGRN   "\x1B[32m" // Green
#define FOREYEL   "\x1B[33m" // Yellow
#define FOREBLU   "\x1B[34m" // Blue
#define FOREMAG   "\x1B[35m" // Magenta
#define FORECYN   "\x1B[36m" // Cyan
#define FOREWHT   "\x1B[37m" // White

/* BACKGROUND */
// These codes set the background color behind the text.
#define BACKBLK   "\x1B[40m" // Black
#define BACKRED   "\x1B[41m" // Red
#define BACKGRN   "\x1B[42m" // Green
#define BACKYEL   "\x1B[43m" // Yellow
#define BACKBLU   "\x1B[44m" // Blue
#define BACKMAG   "\x1B[45m" // Magenta
#define BACKCYN   "\x1B[46m" // Cyan
#define BACKWHT   "\x1B[47m" // White

// These will set the text color and then set it back to normal afterwards.
#define BLK(x) FOREBLK x RESETTEXT
#define RED(x) FORERED x RESETTEXT
#define GRN(x) FOREGRN x RESETTEXT
#define YEL(x) FOREYEL x RESETTEXT
#define BLU(x) FOREBLU x RESETTEXT
#define MAG(x) FOREMAG x RESETTEXT
#define CYN(x) FORECYN x RESETTEXT
#define WHT(x) FOREWHT x RESETTEXT

// Example usage: cout << BLU("This text's color is now blue!") << endl;

// These will set the text's background color then reset it back.
#define BackBLK(x) BACKBLK x RESETTEXT
#define BackRED(x) BACKRED x RESETTEXT
#define BackGRN(x) BACKGRN x RESETTEXT
#define BackYEL(x) BACKYEL x RESETTEXT
#define BackBLU(x) BACKBLU x RESETTEXT
#define BackMAG(x) BACKMAG x RESETTEXT
#define BackCYN(x) BACKCYN x RESETTEXT
#define BackWHT(x) BACKWHT x RESETTEXT

// Example usage: cout << BACKRED(FOREBLU("I am blue text on a red background!")) << endl;

// These functions will set the background to the specified color indefinitely.
// NOTE: These do NOT call RESETTEXT afterwards. Thus, they will set the background color indefinitely until the user executes cout << RESETTEXT
// OR if a function is used that calles RESETTEXT i.e. cout << RED("Hello World!") will reset the background color since it calls RESETTEXT.
// To set text COLOR indefinitely, see SetFore functions below.
#define SetBackBLK BACKBLK
#define SetBackRED BACKRED
#define SetBackGRN BACKGRN
#define SetBackYEL BACKYEL
#define SetBackBLU BACKBLU
#define SetBackMAG BACKMAG
#define SetBackCYN BACKCYN
#define SetBackWHT BACKWHT

// Example usage: cout << SetBackRED << "This text's background and all text after it will be red until RESETTEXT is called in some way" << endl;

// These functions will set the text color until RESETTEXT is called. (See above comments)
#define SetForeBLK FOREBLK
#define SetForeRED FORERED
#define SetForeGRN FOREGRN
#define SetForeYEL FOREYEL
#define SetForeBLU FOREBLU
#define SetForeMAG FOREMAG
#define SetForeCYN FORECYN
#define SetForeWHT FOREWHT

// Example usage: cout << SetForeRED << "This text and all text after it will be red until RESETTEXT is called in some way" << endl;

#define BOLD(x)   "\x1B[1m" x RESETTEXT // Embolden text then reset it.
#define BRIGHT(x) "\x1B[1m" x RESETTEXT // Brighten text then reset it. (Same as bold but is available for program clarity)
#define UNDL(x)   "\x1B[4m" x RESETTEXT // Underline text then reset it.

// Example usage: cout << BOLD(BLU("I am bold blue text!")) << endl;

// These functions will embolden or underline text indefinitely until RESETTEXT is called in some way.

#define SetBOLD   "\x1B[1m" // Embolden text indefinitely.
#define SetBRIGHT "\x1B[1m" // Brighten text indefinitely. (Same as bold but is available for program clarity)
#define SetUNDL   "\x1B[4m" // Underline text indefinitely.

// Example usage: cout << setBOLD << "I and all text after me will be BOLD/Bright until RESETTEXT is called in some way!" << endl;

#endif /* COLORS_HPP */
```

##### 使用方法

```cpp
// 使用后自动恢复默认样式，可嵌套使用
std::cout << BLU("This text's color is now blue!") << std::endl;
std::cout << BACKRED(FOREBLU("I am blue text on a red background!")) << std::endl;
std::cout << BOLD(BLU("I am bold blue text!")) << std::endl;
// 使用后保持当前样式设置
std::cout << SetBackRED << "This text's background and all text after it will be red until RESETTEXT is called in some way" << std::endl;
std::cout << SetForeRED << "This text and all text after it will be red until RESETTEXT is called in some way" << std::endl;
std::cout << SetBOLD << "I and all text after me will be BOLD/Bright until RESETTEXT is called in some way!" << std::endl;
```

#### 简单实现

使用带参数宏定义了字体样式：

```cpp
#ifndef COLORS_HPP
#define COLORS_HPP

//the following are UBUNTU/LINUX, and MacOS ONLY terminal color codes.
#define RESET       "\033[0m"
#define BLACK       "\033[30m"          /* Black */
#define RED         "\033[31m"          /* Red */
#define GREEN       "\033[32m"          /* Green */
#define YELLOW      "\033[33m"          /* Yellow */
#define BLUE        "\033[34m"          /* Blue */
#define MAGENTA     "\033[35m"          /* Magenta */
#define CYAN        "\033[36m"          /* Cyan */
#define WHITE       "\033[37m"          /* White */
#define BOLDBLACK   "\033[1m\033[30m"   /* Bold Black */
#define BOLDRED     "\033[1m\033[31m"   /* Bold Red */
#define BOLDGREEN   "\033[1m\033[32m"   /* Bold Green */
#define BOLDYELLOW  "\033[1m\033[33m"   /* Bold Yellow */
#define BOLDBLUE    "\033[1m\033[34m"   /* Bold Blue */
#define BOLDMAGENTA "\033[1m\033[35m"   /* Bold Magenta */
#define BOLDCYAN    "\033[1m\033[36m"   /* Bold Cyan */
#define BOLDWHITE   "\033[1m\033[37m"   /* Bold White */

#endif /* COLORS_HPP */
```

##### 使用方法

```cpp
// 使用后保持当前样式设置，使用RESET恢复默认样式
std::cout << RED << "Hello World" << RESET << std::endl;
```

### 使用fmt库

```cpp
#include <fmt/color.h>

int main() {
    fmt::print(fg(fmt::color::crimson) | fmt::emphasis::bold, "Hello, {}!\n", "world");
    fmt::print(fg(fmt::color::floral_white) | bg(fmt::color::slate_gray) | fmt::emphasis::underline, "Hello, {}!\n", "мир");
    fmt::print(fg(fmt::color::steel_blue) | fmt::emphasis::italic, "Hello, {}!\n", "世界");
}
```

## 参考

1. [C++文件输入输出-十面埋伏的文章-知乎](https://zhuanlan.zhihu.com/p/346054098)
2. [有效数字和小数位数1-CSDN博客](https://blog.csdn.net/weixin_39484422/article/details/89072133)
3. [有效数字和小数位数2-CSDN博客](https://blog.csdn.net/xiongyangg/article/details/24439295)
4. [文字和底纹样式1-Stack Overflow](https://stackoverflow.com/questions/2616906/how-do-i-output-coloured-text-to-a-linux-terminal)
5. [文字和底纹样式2-Stack Overflow](https://stackoverflow.com/questions/9158150/colored-output-in-c/9158263)
6. [ANSI escape code-Wikipedia](https://en.wikipedia.org/wiki/ANSI_escape_code)
7. [fmtlib/fmt](https://github.com/fmtlib/fmt)
