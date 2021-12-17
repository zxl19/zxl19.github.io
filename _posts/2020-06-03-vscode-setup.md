---
layout: post
title: VS Code配置存档
date: 2020-06-03
author: zxl19
tags: [VS Code, Note]
comments: true
toc: true
pinned: false
---

简单记录一下目前我的VS Code配置，包括编辑器配置和扩展配置。

<!-- more -->

## 编辑器配置

1. 字体：使用等宽字体更加美观，特别是对于代码中空格的宽度和命令行中的命令显示，在Windows下使用默认设置即可，在Linux下可参考Windows使用`monospace`；
2. 双击侧边栏和编辑区边界可以自动调整宽度；

## 扩展配置

扩展配置（按照字母顺序排序）。

### AsciiDoc

为AsciiDoc格式文档提供语言支持。

### Better Comments

根据注释类型生成不同样式的注释。

示例：

```text
// ! 警告类语句（红色）
// ? 疑问类语句（蓝色）
// TODO 待办类语句（橙色）
// * 高亮类语句（绿色）
// // 删除线语句（深灰色）
```

注：在C/C++代码中要谨慎使用高亮类语句。

### Bookmarks

选定行生成书签，可以在书签之间进行跳转。

鼠标右键菜单内操作。

### Bracket Pair Colorizer 2

括号自动配对着色，第二版在匹配速度上有了提升。

**2021年12月：VS Code已包含括号对着色功能，需手动在设置中开启，此扩展已停止维护。**

### C/C++

C/C++语言扩展。

1. 在Windows下会自动安装并配置clang-format；
2. 在Linux下需手动安装并配置clang-format：

   - 安装clang-format：`sudo apt install clang-format`；
   - 配置clang-format：在扩展设置中将`可执行文件的完整路径`设置为`/usr/bin/clang-format`；

### Chinese (Simplified) Language Pack for Visual Studio Code

VS Code中文汉化。

### CMake

CMake语法支持。

### CMake Tools

CMake扩展。

### Code Runner

运行各种语言的代码。

### Code Spell Checker

拼写检查。

### Crypto Tools

提供一系列编码/解码、加密/解密工具，例如base32、SHA512等。目前base64加密中文存在bug，会出现乱码。

### Draw.io Integration

集成Draw.io功能，绘制流程图。

### GitHub Pull Requests and Issues

为VS Code提供GitHub支持。

### GitLens——Git supercharged

增强VS Code内置git的功能，例如对比修改、查看历史记录和显示代码作者。

### Image Preview

代码中引用图片预览。

### indent-rainbow

用不同颜色标识缩进。

### LaTeX Workshop

LaTeX语言扩展，可以预览PDF文档。

### Markdown All in One

Markdown语言扩展。

### Markdown PDF

Markdown文档转PDF文档。

在设置中关闭页眉页脚、选择样式为`github.css`可以获得更好的显示效果。

### Markdown Preview Enhanced

预览、导出Markdown文档。

### markdownlint

Markdown语法检查。

### Matlab

MATLAB语言扩展。

### One Dark Pro

Atom的深色主题，类似的主题还有City Lights theme、Material Theme（会同时安装Material Theme Icon和Community Material Theme）。

在VS Code中通过`Ctrl`+`K`+`Ctrl`+`T`快捷键选择主题。

在设置中打开粗体、关闭斜体可以改善中文注释的显示效果。

### Path Intellisense

文件路径自动补全。

### Polacode

代码截图。

1. `Ctrl`+`Shift`+`P`选择Polacode；
2. 选中要截图的代码；

目前Polacode使用存在一定问题，可以使用CodeSnap或者Polacode-2020作为代替，使用方法同上。

### Python

Python语言扩展，安装Pylance、Jupyter、Jupyter Keymap、Jupyter Notebook Renderers使用增强功能和提高使用体验。

### Rainbow Fart

彩虹屁插件。

### ROS

机器人操作系统（Robot Operating System, ROS）扩展。

### TODO Highlight

高亮`TODO:`和`FIXME:`标识，类似的扩展还有Todo Tree。

示例：

```text
TODO: 待办内容
FIXME: 待修复内容
```

### Trailing Spaces

显示尾部跟随空格。

### vscode-icons

文件图标主题，类似的主题还有Material Icon Theme。

## 参考

1. [空格宽度-CSDN博客](https://bbs.csdn.net/topics/392557784)
2. [VSCode必装的10个高效开发插件-慕课网的文章-知乎](https://zhuanlan.zhihu.com/p/56719281)
3. [如何让VS Code更好用10倍？这里有一份VS Code新手指南-麻瓜编程的文章-知乎](https://zhuanlan.zhihu.com/p/99462672)
4. [第一次使用VS Code时你应该知道的一切配置-千古壹号的文章-知乎](https://zhuanlan.zhihu.com/p/62913725)
5. [自用VSCode优质插件推荐-HanwGeek的文章-知乎](https://zhuanlan.zhihu.com/p/89693351)
6. [vscode必备插件，美化、炫酷、实用-留着防丢-双木珑的文章-知乎](https://zhuanlan.zhihu.com/p/112016680)
7. [一些非常有用的VSCode扩展-Helperhaps的文章-知乎](https://zhuanlan.zhihu.com/p/29553584)
8. [工具篇-vscode效率提升插件-鲲China的文章-知乎](https://zhuanlan.zhihu.com/p/73452541)
9. [那些你应该考虑卸载的VSCode扩展-余腾靖的文章-知乎](https://zhuanlan.zhihu.com/p/125773296)
10. [VSCode插件大全｜VSCode高级玩家之第二篇-三钻的文章-知乎](https://zhuanlan.zhihu.com/p/136428397)
11. [微软再出神器，这次终于对Python下手了！-Jackpop的文章-知乎](https://zhuanlan.zhihu.com/p/154108630)
12. [vscode有哪些让人眼前一亮的插件?-量子位的回答-知乎](https://www.zhihu.com/question/311803609/answer/1296896019)
13. [超越鼓励师for VS Code，写代码不再孤单，有杨超越与你同在-韩骏的文章-知乎](https://zhuanlan.zhihu.com/p/61790645)
14. [太赞了，VSCode上也能画流程图了！-GitHub Daily的文章-知乎](https://zhuanlan.zhihu.com/p/140895359)
15. [实时可视化Debug：VS Code开源新工具，一键解析代码结构](https://zhuanlan.zhihu.com/p/109212146)
16. [Visual Studio Code如何编写运行C、C++程序？-程序员柠檬的回答-知乎](https://www.zhihu.com/question/30315894/answer/1574277687)
17. [Markdown完美转PDF-简书](https://www.jianshu.com/p/4856a78b96b6)
