---
layout: post
title: VS Code配置
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

1. `Editor: Font Family`：设置字体，默认使用等宽字体，对于代码中空格的宽度和命令行中的命令显示更加美观：

    ```text
    'Droid Sans Mono', 'monospace', monospace
    ```

2. `Editor: Word Wrap`：设置超过窗口宽度后是否自动换行，默认关闭，对于Markdown默认开启；
3. `Explorer`->`右键`->勾选`Open Editors`；
4. 双击侧边栏和编辑区边界可以自动调整宽度；

## 扩展配置

```text
Occam's razor: entities should not be multiplied beyond necessity.
奥卡姆剃刀原理：如无必要，勿增实体。
```

扩展配置（按照字母顺序排序），如果在VS Code中安装失败，可以在扩展商店中下载`.vsix`格式的安装包手动安装。

### :emojisense:

在输入emoji时自动补全，emoji格式为`:emoji:`，输入`::`触发提示。

示例：

```text
:smile:
:dog:
```

### AsciiDoc

为AsciiDoc格式文档提供语言支持。

### Better Comments

根据注释类型生成不同样式的注释，类似的扩展还有Colorful Comments。

示例：

```text
// ! Alerts             警告类语句（红色）
// ? Queries            疑问类语句（蓝色）
// TODO TODOs           待办类语句（橙色）
// * Highlights         高亮类语句（绿色）
// // Commented out     删除线语句（深灰色）
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

可以在扩展中指定`clang-format`可执行文件的路径，如果未指定，则会优先使用环境变量中`clang-format`可执行文件的路径；如果未在环境变量中找到，则会使用扩展自带的`clang-format`可执行文件。

### Chinese (Simplified) Language Pack for Visual Studio Code

VS Code中文汉化。

### clangd

C/C++语言自动补全、跳转、函数提示等功能。

1. 按照提示关闭C/C++扩展自带的自动补全；
2. 按照提示安装或更新clangd；
3. 生成`compile_commands.json`文件，供扩展解析；

    - 在`CMakeLists.txt`文件中指定：

        ```cmake
        set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
        ```

    - 在编译时指定：

        ```shell
        cmake .. -DCMAKE_EXPORT_COMPILE_COMMANDS=1
        ```

    - 建议将生成的`compile_commands.json`文件放到工程顶层目录或者`build`文件夹中；

### CMake

CMake语法支持。

### CMake Tools

CMake扩展。

### cmake-format

格式化`CMakeLists.txt`文件。

1. 安装`cmakelang`格式化工具：

    ```shell
    python3 -m pip install cmakelang
    ```

2. 在`CMakeLists.txt`文件中`右键`->`Format Document`；

### Code Runner

运行各种语言的代码。

### Code Spell Checker

拼写检查。

### Compare Folders

按照内容比较文件夹，并排显示文件夹中的文件内容差异。可以用于代替Beyond Compare和CC Compare的功能。

### Crypto Tools

提供一系列编码/解码、加密/解密工具，例如base32、SHA512等。目前base64加密中文存在bug，会出现乱码。

鼠标右键菜单内操作。

### Doxygen Documentation Generator

按照Doxygen格式生成C++文件注释和函数注释。

1. 在设置中设置作者姓名和作者电子邮箱；
2. 输入`/**`后回车自动生成注释；

### Draw.io Integration

集成Draw.io功能，绘制流程图。

在设置中将主题设置为`Kennedy`可以获得更好的显示效果。

### GitHub Pull Requests and Issues

为VS Code提供GitHub支持。

### gitignore

从[github/gitignore](https://github.com/github/gitignore)仓库中拉取`.gitignore`文件模板。

1. `Ctrl`+`Shift`+`P`，选择`Add gitignore`；
2. 选择语言，在工程根目录下创建`.gitignore`文件；

### GitLens——Git supercharged

增强VS Code内置Git的功能，例如对比修改、查看历史记录和显示代码作者。

### Image Preview

代码中引用图片预览。

### indent-rainbow

用不同颜色标识缩进。

### IntelliCode

为Python、TypeScript/JavaScript、Java提供基于上下文和机器学习的自动补全，安装IntelliCode API Usage Examples扩展可以查看GitHub中的用法示例并提高使用体验，类似的扩展还有Tabnine AI Autocomplete、GitHub Copilot、Kite。

**2022年11月：Kite已停止维护。**

### koroFileHeader

生成文件头部注释和函数注释，类似的扩展还有vscode-fileheader、autoDocstring。

详细配置选项说明参考[Wiki](https://github.com/OBKoro1/koro1FileHeader/wiki)。

1. 文件头部注释：

    - 配置`fileheader.configObj`关闭自动添加文件头部注释，示例：

        ```json
        "fileheader.customMade": {
            "autoAdd": false
        }
        ```

    - 配置`fileheader.customMade`指定文件头部注释格式，示例：

        ```json
        "fileheader.customMade": {
            "Author": "git config user.name && git config user.email",
            "Date": "Do not edit",
            "Description": "",
            "custom_string_obkoro1_copyright": "Copyright (c) ${now_year} by git config user.name && git config user.email, All Rights Reserved."
        }
        ```

    - 快捷键：`Ctrl`+`Super`+`T`；

2. 函数注释：

    - 配置`fileheader.cursorMode`指定函数注释格式，示例：

        ```json
        "fileheader.cursorMode": {
            "description": "",
            "param": "",
            "return": ""
        }
        ```

    - 快捷键：`Ctrl`+`Super`+`I`；

3. 注释图案：

    - 选择注释图案：`Ctrl`+`Shift`+`P`，输入`codeDesign`选择；
    - 快捷键：`Ctrl`+`Super`+`J`；

### LaTeX Workshop

LaTeX语言扩展，配置`latex-workshop.latex.tools`、`latex-workshop.latex.recipes`后可以编译文档并预览。

1. `latex-workshop.latex.tools`指定了单条编译命令的参数，示例：

    ```json
    {
        "name": "xelatexmk",
        "command": "latexmk",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-xelatex",
            "-outdir=%OUTDIR%",
            "%DOC%"
        ],
        "env": {}
    }
    ```

2. `latex-workshop.latex.recipes`指定了多条编译命令的执行顺序，示例：

    ```json
    {
        "name": "xelatex ➞ biber ➞ xelatex × 2",
        "tools": [
            "xelatexmk",
            "biber",
            "xelatexmk",
            "xelatexmk"
        ]
    }
    ```

### Luna Paint——Image Editor

图片编辑扩展，支持多种图片格式。

### Markdown All in One

Markdown语言扩展。

1. 快捷键：

    | 功能 | 快捷键 |
    | :--- | :--- |
    | 切换粗体 | `Ctrl`+`B` |
    | 切换斜体 | `Ctrl`+`I` |
    | 切换删除线 | `Alt`+`S` |
    | 标题升级 | `Ctrl`+`Shift`+`]` |
    | 标题降级 | `Ctrl`+`Shift`+`[` |
    | 切换数学环境 | `Ctrl`+`M` |
    | 切换勾选 | `Alt`+`C` |
    | 预览 | `Ctrl`+`Shift`+`V` |
    | 侧边预览 | `Ctrl`+`K`+`V` |

2. 生成目录：

    - `Ctrl`+`Shift`+`P`，选择`Markdown All in One: Create Table of Contents`；
    - 目录在文件保存时自动更新；

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

Atom的深色主题，类似的主题还有City Lights theme、Material Theme（会同时安装Community Material Theme和Material Theme Icons）。

在VS Code中通过`Ctrl`+`K`+`Ctrl`+`T`快捷键选择主题。

在设置中打开粗体、关闭斜体可以改善中文注释的显示效果。

### Path Intellisense

文件路径自动补全，类似的扩展还有Path Autocomplete。

### Pip Manager

管理Python包，提供安装、删除、搜索、升级、指定版本等功能。

### Polacode

代码截图。

1. `Ctrl`+`Shift`+`P`，选择`Polacode`；
2. 选中要截图的代码；

**目前Polacode使用存在一定问题，可以使用CodeSnap或者Polacode-2022作为代替，使用方法同上。**

### Pomodoro

番茄工作法。

### Power Mode

在输入时添加炫酷的特效。

1. 在设置中开启扩展；
2. 在设置中关闭振动特效，可以获得更好的显示效果。

### Project Manager

管理项目工程，实现快速切换。

1. 打开需要管理的项目工程，并将其保存到收藏夹中：

    - 方法一：`Ctrl`+`Shift`+`P`，输入`Project Manager: Save Project`；
    - 方法二：在侧边栏中点击保存图标；

2. 修改`projects.json`文件，添加标签：

    - 方法一：`Ctrl`+`Shift`+`P`，输入`Project Manager: Edit Projects`；
    - 方法二：在侧边栏中点击编辑图标；

    示例：

    ```json
    {
        "name": "zxl19.github.io",
        "rootPath": "/home/zxl19.github.io",
        "paths": [],
        "tags": [
            "zxl19"
        ],
        "enabled": true
    }
    ```

### Python

Python语言扩展，安装Pylance、Pylint、isort、Jupyter（包括Jupyter Cell Tags、Jupyter Keymap、Jupyter Notebook Renderers、Jupyter Slide Show）等扩展可以使用增强功能并提高使用体验。

在设置中开启使用Pylint可以使用指定的静态分析工具。

### Rainbow Fart

彩虹屁扩展。

### ROS

机器人操作系统（Robot Operating System, ROS）扩展。

### shell-format

格式化shell脚本、Dockerfile、`.gitignore`文件等，类似的扩展还有Bash Beautify。

### ShellCheck

对于shell脚本进行静态语法分析。

### shellman

对于shell脚本进行自动补全。

### Super ChatGPT

免费使用ChatGPT，每天限制20次。

### Todo Tree

高亮注释中的标签并且以树的形式显示，类似的扩展还有TODO Highlight。

在设置中打开使用配色方案可以获得更好的显示效果。

示例：

```text
BUG     a known bug that should be corrected.   存在的BUG（红色）
HACK    a workaround.                           应变方法、变通方法（橙色）
FIXME   should be corrected.                    待修复内容（黄色）
TODO    something to be done.                   待办内容（绿色）
XXX     warn other programmers of problematic   警告需要改进的代码（蓝色）
        or misguiding code, "dirty code" that
        needs improving.
[ ]     an uncompleted task                     未完成任务（紫色）
[x]     a completed task                        已完成任务（粉色）
```

### Toggle Zen Mode

添加进入禅模式（zen mode）的按钮。

1. 禅模式快捷键：`Ctrl`+`K`+`Z`；
2. 全屏快捷键：`F11`；

### Trailing Spaces

显示尾部跟随空格。

### Typora

原名为vscode-office，支持预览PDF、Excel等格式的办公文档，并提供所见即所得（What You See Is What You Get，WYSIWYG）的Markdown编辑器功能。

### Typst LSP

Typst语言扩展。

### vscode-icons

文件图标主题，类似的主题还有Material Icon Theme和Material Theme Icons。

### vscode-mindmap

绘制思维导图，类似的扩展还有Markmap。

## 配置文件查看和修改

1. 对于编辑器和插件的设置都会保存在`settings.json`配置文件中；
2. `Ctrl`+`Shift`+`P`，输入`Preferences: Open User Settings (JSON)`进行查看和修改；
3. 删除`settings.json`配置文件中大括号`{}`内部的内容可以将VS Code恢复默认设置；

## 快捷键速查表

1. [Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)
2. [Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
3. [macOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

## 参考

1. [空格宽度-CSDN博客](https://bbs.csdn.net/topics/392557784)
2. [VSCode必装的10个高效开发插件-慕课网的文章-知乎](https://zhuanlan.zhihu.com/p/56719281)
3. [如何让VS Code更好用10倍？这里有一份VS Code新手指南-麻瓜编程的文章-知乎](https://zhuanlan.zhihu.com/p/99462672)
4. [第一次使用VS Code时你应该知道的一切配置-千古壹号的文章-知乎](https://zhuanlan.zhihu.com/p/62913725)
5. [自用VSCode优质插件推荐-HanwGeek的文章-知乎](https://zhuanlan.zhihu.com/p/89693351)
6. [vscode必备插件，美化、炫酷、实用-留着防丢-双木珑的文章-知乎](https://zhuanlan.zhihu.com/p/112016680)
7. [一些非常有用的VSCode扩展-Helperhaps的文章-知乎](https://zhuanlan.zhihu.com/p/29553584)
8. [工具篇-vscode效率提升插件-鲲China的文章-知乎](https://zhuanlan.zhihu.com/p/73452541)
9. [VSCode插件大全｜VSCode高级玩家之第二篇-三钻的文章-知乎](https://zhuanlan.zhihu.com/p/136428397)
10. [vscode有哪些让人眼前一亮的插件?-韦易笑的回答-知乎](https://www.zhihu.com/question/311803609/answer/2387914071)
11. [Visual Studio Code如何编写运行C、C++程序？-程序员柠檬的回答-知乎](https://www.zhihu.com/question/30315894/answer/1574277687)
12. [vscode实用插件推荐-很酷的程序员的文章-知乎](https://zhuanlan.zhihu.com/p/441608260)
13. [vscode有没有性能优化插件？-秃头披风侠cc的回答-知乎](https://www.zhihu.com/question/441992533/answer/2430995843)
14. [那些你应该考虑卸载的VSCode扩展-余腾靖的文章-知乎](https://zhuanlan.zhihu.com/p/125773296)
15. [微软再出神器，这次终于对Python下手了！-Jackpop的文章-知乎](https://zhuanlan.zhihu.com/p/154108630)
16. [vscode有哪些让人眼前一亮的插件?-量子位的回答-知乎](https://www.zhihu.com/question/311803609/answer/1296896019)
17. [超越鼓励师for VS Code，写代码不再孤单，有杨超越与你同在-韩骏的文章-知乎](https://zhuanlan.zhihu.com/p/61790645)
18. [太赞了，VSCode上也能画流程图了！-GitHub Daily的文章-知乎](https://zhuanlan.zhihu.com/p/140895359)
19. [实时可视化Debug：VS Code开源新工具，一键解析代码结构](https://zhuanlan.zhihu.com/p/109212146)
20. [Markdown完美转PDF-简书](https://www.jianshu.com/p/4856a78b96b6)
21. [Visual Studio会被VS Code及各种插件取代吗？-知乎](https://www.zhihu.com/question/277139137/answer/1657100889)
22. [使用clangd替代c/c++配置vscode c++项目-smallsunsun的文章-知乎](https://zhuanlan.zhihu.com/p/145430576)
23. [最终，我看向了clangd-小钻风的文章-知乎](https://zhuanlan.zhihu.com/p/364518020)
24. [cxasm/cc-compare](https://github.com/cxasm/cc-compare)
25. [YKB2333/Beyond-Compare](https://github.com/YKB2333/Beyond-Compare)
26. [OBKoro1/koro1FileHeader](https://github.com/OBKoro1/koro1FileHeader)
27. [Comment (computer programming)-Wikipedia](https://en.wikipedia.org/wiki/Comment_(computer_programming))
28. [typst/typst](https://github.com/typst/typst)
29. [nvarner/typst-lsp](https://github.com/nvarner/typst-lsp)
30. [当你上班可以摸鱼的时候可以做些什么？-程序员阿德的回答-知乎](https://www.zhihu.com/question/365629693/answer/2127925726)
31. [装上这几个VSCode插件后，上班划水摸鱼不是梦-GitHub Daily的文章-知乎](https://zhuanlan.zhihu.com/p/58302580)
32. [炸裂！VSCode 摸鱼神器！！！-YYds的文章-知乎](https://zhuanlan.zhihu.com/p/408767088)
33. [VS CODE恢复出厂设置-bilibili](https://www.bilibili.com/video/BV12B4y1479v)
34. [Kite is saying farewell](https://www.kite.com/blog/product/kite-is-saying-farewell/)
