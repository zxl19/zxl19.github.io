---
layout: post
title: LaTeX使用笔记
date: 2021-03-29
author: zxl19
tags: [LaTeX, Note]
comments: true
toc: true
pinned: false
---

我的$\LaTeX$使用笔记及格式约定。

<!-- more -->

## 基础设置

```latex
% !TeX encoding = UTF-8
% !TeX program = xelatex
% !TeX spellcheck = en_US
```

## 常用宏包

```latex
\usepackage{amsmath,amsthm,amsfonts,amssymb,amscd}  % 数学公式、符号等宏包
\usepackage{enumerate}              % 插入带序号列表
\usepackage{graphicx}               % 插入图片
\usepackage{listings}               % 插入代码块

\usepackage{hyperref}               % 插入超链接，官方文档建议在最后调用
\usepackage[backref]{hyperref}      % 章节引回
\usepackage[pagebackref]{hyperref}  % 页码引回
\hypersetup{                        % 超链接样式设置
    colorlinks=false,
    linkcolor=blue,
    linkbordercolor={0 0 1}
}
\hypersetup{hidelinks}              % 不显示超链接线框

\usepackage{ctex}                   % 中文支持
\usepackage{mathtools}              % 插入分段函数

\usepackage{algorithm}              % 插入伪代码
\usepackage{algpseudocode}          % 插入伪代码
\renewcommand{\algorithmicrequire}{\textbf{Input:}} % Use Input in the format of Algorithm
\renewcommand{\algorithmicensure}{\textbf{Output:}} % Use Output in the format of Algorithm

\usepackage[framed,numbered,autolinebreaks,useliterate]{mcode}  % 插入MATLAB代码块，基于listings开发
\usepackage{multirow}               % 跨多行表格
\usepackage{subfigure}              % 插入子图

\usepackage{tabto}                  % 插入Tab
\NumTabs{16}                        % define 16 equally spaced tabs starting at the left margin
                                    % and spanning \linewidth

\usepackage{fontawesome}            % 添加小图标

\usepackage{pifont}                 % 添加对号、错号
\newcommand{\cmark}{\ding{51}}      % 定义对号命令，本质上是重命名pifont宏包中的\ding{51}命令
\newcommand{\xmark}{\ding{55}}      % 定义错号命令，本质上是重命名pifont宏包中的\ding{55}命令

\usepackage[square,super]{natbib}   % 调整参考文献样式：方括号、右上角

\usepackage[landscape]{geometry}    % 设置页面为横向

\usepackage{tikz}                   % 绘制图形
\usepackage{tikz-3dplot}            % 绘制三维坐标系，坐标变换

\usepackage{courier}                % 使用打字机字体/等宽字体

\usepackage{placeins}               % 限制浮动体位置

\usepackage{siunitx}                % 使用国际单位制
```

## 格式约定

1. 源码在遇到`\begin{}`时要缩进；
2. 数学符号参考[常用数学符号的LaTeX表示方法](https://mohu.org/info/symbols/symbols.htm)，但有以下几点注意事项：

    - 上下标使用`{}`括起来；
    - 矩阵和向量使用粗体（boldface）：`\mathbf{}`或`\boldsymbol{}`；
    - 常数使用正体，也被称为罗马体（roman）：`\mathrm{}`；
    - 数集使用黑板粗体（blackboard bold）：`\mathbb{}`；
    - 坐标系使用书法体（calligraphic）：`\mathcal{}`；
    - 一些特殊符号使用哥特体，也被称为德文尖角体（fraktur）：`\mathfrak{}`；
    - 绝对值使用`|`或`\vert`，范数使用`\|`；
    - argmin使用`\mathop{\arg\min}\limits_{}`，argmax同理；
    - 小空格用`\quad`，大空格用`\qquad`；
    - 分式尽量使用`\dfrac{}{}`，若显示有问题再使用`\frac{}{}`；
    - 角度使用`\angle`，度数使用`^{\circ}`；
    - 点乘使用`\cdot`或`\bullet`，叉乘使用`\times`；
    - 导数使用`\mathrm{d}`，偏导数使用`\partial`；
    - 反对称矩阵使用`^{\wedge}`，其逆运算使用`^{\vee}`；
    - 矩阵转置使用`^{\mathrm{T}}`；
    - 一阶导数使用`^{\prime}`；
    - 定义等号使用`\triangleq`或`\overset{def}{=}`；
    - 内容上加长横线使用`\overline{}`；
    - 内容上加文字使用`\overset{}{}`；
    - 公式上方大括号使用`\overbrace{}^{}`，公式下方大括号使用`\underbrace{}_{}`；
    - 向上取整使用`\lceil \rceil`、向下取整使用`\lfloor \rfloor`；

3. 括号大小根据内容自动调整：

    ```latex
    \left(          \right)         % 小括号()
    \left[          \right]         % 中括号[]
    \left\{         \right\}        % 大括号{}
    \left|          \right|         % 绝对值||
    \left\|         \right\|        % 范数
    \left.          \right|         % 左侧不显示，右侧大小自动调整
    \left\lceil     \right\rceil    % 向上取整⌈⌉
    \left\lfloor    \right\rfloor   % 向下取整⌊⌋
    ```

4. 使用`\hfill`进行水平填充，同理，使用`\vfill`进行垂直填充；
5. 使用`\hspace{}`插入水平间隔，同理，使用`\vspace{}`插入垂直间隔，大括号前添加`*`表示强制插入；
6. 使用`\tab`插入`Tab`，一个`Tab`对应的宽度通过`\NumTabs{}`进行定义，将当前环境下的行宽若干等分；
7. 公式、图片、表格的引用标记要进行区分：

    ```latex
    \label{eq:XXX}      % 公式
    \label{fig:XXX}     % 图片
    \label{tab:XXX}     % 表格
    ```

8. 插入对号、错号：

    ```latex
    \cmark              % 对号
    \xmark              % 错号
    ```

9. 使用`\today`插入当天日期；
10. 使用`\ `或`{}`在$\LaTeX$命令后插入空格；
11. 字母音调：

    ```latex
    \={}                % 一声
    \'{}                % 二声
    \v{}                % 三声
    \u{}                % 类似三声的圆弧
    \`{}                % 四声
    \.{}                % 加点
    \"{}                % 加双点
    ```

12. 电子邮箱名使用等宽字体，也被称为打字机字体（teletype）：`\texttt{}`；

## 自定义命令

```latex
\newcommand{命令名}[参数个数][默认参数]{命令定义}       % 定义新命令，要求新命令名不能与已有命令重名
\renewcommand{命令名}[参数个数][默认参数]{命令定义}     % 重命名命令，要求被重命名的命令存在
\providecommand{命令名}[参数个数][默认参数]{命令定义}   % 条件定义命令，如果命令不存在则定义新命令，此时效果与\newcommand相同，如果命令已存在则无操作

% 要求参数不超过一段
\newcommand*{命令名}[参数个数][默认参数]{命令定义}
\renewcommand*{命令名}[参数个数][默认参数]{命令定义}
\providecommand*{命令名}[参数个数][默认参数]{命令定义}
```

1. 命令名不能以`\end`开头；
2. 参数个数不能超过9个，缺省表示无参数输入；
3. 默认参数：

    - 在定义命令时，默认参数只能指定第一个参数的默认值，`[]`表示默认参数为空字符串，缺省表示无默认参数；
    - 在调用命令时，对于第一个参数，可以通过新参数覆盖默认参数，`[]`表示新参数为空字符串，缺省表示使用默认参数；
    - 在调用命令时，如果定义了默认参数，其余参数从第二个参数开始输入；

4. 命令定义中使用`#n`表示第n个参数；

示例：

```latex
\newcommand{\RS}{Robin Smith}
\newcommand{\qedsymbol}{\small QED}
\newcommand{\defref}[1]{Definition~\ref{#1}}
\newcommand{\salutation}[1][Sir or Madam]{Dear #1:}
```

## 字体

### 字体样式

1. 粗体（boldface）：`\textbf{}`；
2. 意大利斜体（italics）：`\textit{}`；
3. 倾斜正体（slanted）：`\textsl{}`；
4. 打字机字体（teletype）：`\texttt{}`；
5. 下划线（underline）：`\underline{}`；

### 字体大小

#### 全局模式

在文档开头定义默认字体大小：

```latex
\documentclass[12pt]{article}
```

#### 局部模式

在全局模式的基础上修改字体大小：

```latex
\tiny           % 最小
\scriptsize
\footnotesize
\small
\normalsize     % 默认字体大小
\large
\Large
\LARGE
\huge
\Huge           % 最大
```

## 列表

### 无序号列表

```latex
\begin{itemize} % 默认：实心点
    \item       默认样式
    \item[*]    指定样式
\end{itemize}
```

### 有序号列表

```latex
\begin{enumerate}[(1)] % 此处指定序号样式，默认：1.
    \item 支持123
    \item 支持abc
    \item 支持ABC
    \item 支持i ii iii
    \item 支持I II III
    \item 在上述基础上支持左右括号
\end{enumerate}
```

## 公式

### 行内公式

```latex
$公式内容$
```

### 行间公式

#### 带编号

##### 单个公式

```latex
\begin{equation}
    \label{eq:1.1} % 引用标记
    公式内容
\end{equation}
```

##### 多个公式

###### 分别编号

```latex
\begin{align}
    \label{eq:1.2}
    & 公式内容 \\
    \label{eq:1.3}
    & 公式内容
\end{align}
```

###### 相同编号

```latex
\begin{equation}
    \label{eq:1.4}
    \begin{aligned}
        & 公式内容 \\
        & 公式内容
    \end{aligned}
\end{equation}
```

##### 公式引用

```latex
\eqref{eq:1.1}   % 有括号
\ref{eq:1.2}     % 无括号
```

#### 无编号

```latex
\begin{align*}
    & 公式内容 \\
    & 公式内容
\end{align*}
```

#### 分段函数

通常在`equation`或`align`环境中使用，对于大括号整体编号。

1. 使用`dcases`：

    ```latex
    \begin{dcases}
        公式内容 & 条件 \\
        公式内容 & 条件
    \end{dcases}
    ```

    - `dcases`：条件为纯公式，文本使用`\text{}`；
    - `dcases*`：条件为纯文本，公式使用`$ $`；

2. 使用`array`：

    ```latex
    \left\{\begin{array}{l}
        公式内容 \\
        公式内容
    \end{array}\right.
    ```

#### 向量/矩阵

##### 使用`array`环境

```latex
\begin{array}{ccc} % 指定每列的对齐方式，个数对应列数
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
\end{array}
```

1. 对齐方式：

    - `c`：center，居中；
    - `l`：left，左对齐；
    - `r`：right，右对齐；

2. 列之间可以添加分隔线`|`；

##### 使用矩阵环境

```latex
\begin{bmatrix} % 矩阵样式
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
\end{bmatrix}
```

1. 矩阵样式：

    - `matrix`：无括号；
    - `pmatrix`：圆括号；
    - `bmatrix`：方括号；
    - `Bmatrix`：大括号；
    - `vmatrix`：行列式；
    - `Vmatrix`：范数；

## 图片

### 插入单个图片

```latex
\begin{figure}[htbp] % 指定图片位置
    \centering % 居中
    \includegraphics[width=10cm]{image.png}
    \caption{Image Title} % 图片标题
    \label{fig:1}
\end{figure}
```

1. 浮动格式说明：

    - `h`：here，当前位置；
    - `t`：top，顶部；
    - `b`：bottom，底部；
    - `p`：page of its own，浮动页；

2. 强制浮动格式：`[!h]`，不考虑美观性；
3. 使用`\FloatBarrier`限制浮动体位置；
4. 图片格式说明：

    - 建议矢量图片使用`.pdf`格式，比如数据可视化的绘图；
    - 照片应使用`.jpg`格式；
    - 其他的栅格图应使用无损的`.png`格式；
    - 注意，$\LaTeX$不支持`.tiff`格式，`.eps`格式已经过时；

5. 图片跨双栏使用`\begin{figure*}`；

### 插入子图

以四个子图2*2排列为例进行说明：

```latex
\begin{figure}[htbp]
    \centering
    \subfigure[Subfigure Title 1] % 子图标题
    {
        \includegraphics[width=0.3\textwidth]{image1.png}
        \label{fig:2a}
    }
    \quad
    \subfigure[Subfigure Title 2]
    {
        \includegraphics[width=0.3\textwidth]{image2.png}
        \label{fig:2b}
    }
    % 这里换行

    \subfigure[Subfigure Title 3]
    {
        \includegraphics[width=0.3\textwidth]{image3.png}
        \label{fig:2c}
    }
    \quad
    \subfigure[Subfigure Title 4]
    {
        \includegraphics[width=0.3\textwidth]{image4.png}
        \label{fig:2d}
    }
    \caption{Title} % 总标题
    \label{fig:2}
\end{figure}
```

## 表格

```latex
\begin{table}[htbp] % 指定表格位置
    % \def\arraystretch{1.3} % 调整表格整体行高
    \centering
    \caption{Table Title} % 表格标题
    \label{tab:1}
    \begin{tabular}{ccc} % 指定每列的对齐方式，个数对应列数
        \hline
        方法 & APE [m] & RPE [\%]\\
        \hline
        方法1 & 0.10 & 0.20 \\
        方法2 & 0.05 & 0.15 \\
        \hline
    \end{tabular}
\end{table}
```

1. 浮动格式说明同上；
2. 对齐方式：

    - `c`：center，居中；
    - `l`：left，左对齐；
    - `r`：right，右对齐；
    - `p{}`：超过指定宽度后自动换行，例如：`p{3cm}`；

3. 表格框线：

    - 水平框线：使用`\hline`；
    - 垂直框线：在对齐方式处对应的列之间添加分隔线`|`；
    - 部分列水平框线：使用`\cline{i-j}`在i到j列间添加水平框线，使用`\rule{0pt}{11pt}`调节垂直方向距离；

4. 表格跨双栏使用`\begin{table*}`；
5. 不规则形状表格：

    ```latex
    \multicolumn{number of cols}{pos}{text} % 跨多列，pos表示对齐方式
    \multirow{number of rows}{width}{text}  % 跨多行，宽度不定可用{*}
    ```

## 超链接

### 网址超链接

```latex
\url{网址}              % 直接显示待超链接的网址
\href{网址}{显示文字}   % 显示带超链接的文字
```

### 邮箱超链接

```latex
\href{mailto:xxx@xxx.xxx}{显示文字}
```

## 伪代码

```latex
\begin{algorithm}[htbp]
    \caption{Title} % 伪代码标题
    \label{alg:1}
    \begin{algorithmic}[1]
    \If{condition}
    \State statement
    \ElsIf{condition}
    \State statement
    \ForAll{condition}
    \If{condition}
    \State statement
    \EndIf
    \EndFor
    \State statement
    \EndIf
    \State \Return return value
    \end{algorithmic}
\end{algorithm}
```

## 代码块

### 常用语言支持

1. bash
2. C
3. C++
4. Matlab
5. Octave
6. Python
7. TeX

### 设置显示样式

```latex
\definecolor{codegreen}{rgb}{0,0.6,0}
\definecolor{codegray}{rgb}{0.5,0.5,0.5}
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\definecolor{backcolour}{rgb}{0.95,0.95,0.92}

\lstdefinestyle{mystyle}{
    backgroundcolor=\color{backcolour},
    commentstyle=\color{codegreen},
    keywordstyle=\color{blue}\bfseries,
    numberstyle=\tiny\color{codegray},
    stringstyle=\color{codepurple},
    basicstyle=\ttfamily\footnotesize,
    breakatwhitespace=false,
    breaklines=true,
    captionpos=b,
    keepspaces=true,
    numbers=left,
    numbersep=5pt,
    showspaces=false,
    showstringspaces=false,
    showtabs=false,
    tabsize=4,
    frame=shadowbox,
    framerule=0.5pt,
    otherkeywords={string}
}
```

### 插入代码块

#### 直接插入

```latex
\lstset{style=mystyle} % 使用显示样式
\begin{lstlisting}[language=语言]
代码段
\end{lstlisting}
```

示例：

```latex
\lstset{style=mystyle}
\begin{lstlisting}[language=C++]
#include <iostream>
using namespace std;

int main()
{
    // This is a comment.
    cout << "Hello, World!" << endl;
    return 0;
}
\end{lstlisting}
```

#### 从文件插入

```latex
\lstset{style=mystyle} % 使用显示样式
\lstinputlisting[language=语言]{文件名}
```

示例：

```latex
\lstset{style=mystyle} % 使用显示样式
\lstinputlisting[language=C++]{main.cpp}
```

## 脚注

```latex
\footnote{脚注内容}         % 编号自动递增
\footnote[编号]{脚注内容}   % 人为指定编号（纯数字）
```

## 引用参考文献

### 不使用BibTeX

#### 文献保存

在文章末尾插入：

```latex
\begin{thebibliography}{99} % 最大参考文献个数

\bibitem{标签}参考文献引用格式 % 标签在引用时使用

\end{thebibliography}
```

示例：

```latex
\begin{thebibliography}{99}

\bibitem{ref1}Zhang J, Singh S. LOAM: Lidar Odometry and Mapping in Real-time[C]//Robotics: Science and Systems. 2014, 2(9).
\bibitem{ref2}Zhang J, Singh S. Low-drift and real-time lidar odometry and mapping[J]. Autonomous Robots, 2017, 41(2): 401-416.
\bibitem{ref3}Shan T, Englot B. Lego-loam: Lightweight and ground-optimized lidar odometry and mapping on variable terrain[C]//2018 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2018: 4758-4765.
\bibitem{ref4}Shan T, Englot B, Meyers D, et al. Lio-sam: Tightly-coupled lidar inertial odometry via smoothing and mapping[J]. arXiv preprint arXiv:2007.00258, 2020.

\end{thebibliography}
```

#### 文献引用

```latex
\cite{ref1}
\cite{ref2, ref3}
```

### 使用BibTeX

#### 文献保存

1. 保存`.bib`文件：

    ```latex
    @article{name1, % 名称在引用时使用
    author = {作者, 多个作者用 and 连接, 多个词当成一个整体用{}括起来, 例如团体名和组织名},
    title = {标题},
    journal = {期刊名},
    volume = {卷},
    number = {页码},
    year = {年份},
    abstract = {摘要, 引用时自己参考, 非必须}
    }
    @book{name2,
    author ="作者",
    year="年份",
    title="书名",
    publisher ="出版社名称"
    }
    ```

    示例：

    ```latex
    @inproceedings{zhang2014loam,
        title={LOAM: Lidar Odometry and Mapping in Real-time.},
        author={Zhang, Ji and Singh, Sanjiv},
        booktitle={Robotics: Science and Systems},
        volume={2},
        number={9},
        year={2014}
    }
    @article{zhang2017low,
    title={Low-drift and real-time lidar odometry and mapping},
    author={Zhang, Ji and Singh, Sanjiv},
    journal={Autonomous Robots},
    volume={41},
    number={2},
    pages={401--416},
    year={2017},
    publisher={Springer}
    }
    @inproceedings{shan2018lego,
    title={Lego-loam: Lightweight and ground-optimized lidar odometry and mapping on variable terrain},
    author={Shan, Tixiao and Englot, Brendan},
    booktitle={2018 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
    pages={4758--4765},
    year={2018},
    organization={IEEE}
    }
    @article{shan2020lio,
    title={Lio-sam: Tightly-coupled lidar inertial odometry via smoothing and mapping},
    author={Shan, Tixiao and Englot, Brendan and Meyers, Drew and Wang, Wei and Ratti, Carlo and Rus, Daniela},
    journal={arXiv preprint arXiv:2007.00258},
    year={2020}
    }
    ```

2. 在文章末尾插入：

    ```latex
    \bibliographystyle{plain}   % 预设样式
    \bibliography{ref}          % 对应.bib文件名
    ```

3. 预设样式说明：

    - `plain`：按字母的顺序排列，比较次序为作者、年度和标题；
    - `unsrt`：样式同`plain`，只是按照引用的先后排序；
    - `alpha`：用作者名首字母+年份后两位作标号，以字母顺序排序；
    - `abbrv`：类似`plain`，将月份全拼改为缩写，更显紧凑；
    - `ieeetr`：国际电气电子工程师协会期刊样式；
    - `acm`：美国计算机学会期刊样式；
    - `siam`：美国工业和应用数学学会期刊样式；
    - `apalike`：美国心理学学会期刊样式；

#### 文献引用

```latex
\cite{name1}
\cite{name1, name2}
```

#### 文献格式化工具

##### `.bib`文件格式化

1. [yuchenlin/rebiber](https://github.com/yuchenlin/rebiber)
2. [MLNLP-World/SimBiber](https://github.com/MLNLP-World/SimBiber)

##### 引用样式格式化

1. [zepinglee/gbt7714-bibtex-style](https://github.com/zepinglee/gbt7714-bibtex-style)
2. [Haixing-Hu/GBT7714-2005-BibTeX-Style](https://github.com/Haixing-Hu/GBT7714-2005-BibTeX-Style)

## TikZ绘图

- [x] 单独整理。

## Beamer演示文稿

- [ ] 单独整理。

## 高质量网站存档

### 提升输入效率

#### LaTeX数学公式

##### 数学符号

1. [常用数学符号的LaTeX表示方法](https://mohu.org/info/symbols/symbols.htm)
2. [List of LaTeX mathematical symbols-OeisWiki](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)
3. [LaTeX Mathematical Symbols-Rice University](https://www.caam.rice.edu/~heinken/latex/symbols.pdf)
4. [Detexify](http://detexify.kirelabs.org/classify.html)

##### 公式编辑器

1. [LaTeX公式编辑器](https://www.latexlive.com)
2. [Equation Editor](https://editor.codecogs.com)
3. [在线LaTeX公式编辑器](https://latex.codecogs.com/eqneditor/editor.php?lang=zh-cn)
4. [LaTeX在线：吴文中数学公式编辑器](https://latex.91maths.com)
5. [公式王](https://gongshi.wang)
6. [google/latexify_py](https://github.com/google/latexify_py)
7. [blaisewang/img2latex-mathpix](https://github.com/blaisewang/img2latex-mathpix)

##### 数学笔记

1. [gillescastel/latex-snippets](https://github.com/gillescastel/latex-snippets)
2. [gillescastel/university-setup](https://github.com/gillescastel/university-setup)

#### Office数学公式

1. [LaTeX to MathML](https://osanshouo.github.io/latex2mathml-web/index.html)
2. [LaTeX to MathML](https://tmke8.github.io/math-core/)
3. [Temml](https://temml.org)
4. [IguanaTex](http://www.jonathanleroux.org/software/iguanatex/)
5. [Jonathan-LeRoux/IguanaTex](https://github.com/Jonathan-LeRoux/IguanaTex)
6. [idf/LaTex2Word-Equation](https://github.com/idf/LaTex2Word-Equation)
7. [ronkok/Temml](https://github.com/ronkok/Temml)
8. [xiaoyvyv/LatexToMathML](https://github.com/xiaoyvyv/LatexToMathML)
9. [osanshouo/latex2mathml](https://github.com/osanshouo/latex2mathml)
10. [tmke8/math-core](https://github.com/tmke8/math-core)

#### 表格

1. [Tables Generator](https://www.tablesgenerator.com)
2. [excel2latex-CTAN](https://www.ctan.org/tex-archive/support/excel2latex)

#### 中文支持

1. [CTeX-org/ctex-kit](https://github.com/CTeX-org/ctex-kit)
2. [Haixing-Hu/latex-chinese-fonts](https://github.com/Haixing-Hu/latex-chinese-fonts)

#### 代码格式化

1. [LaTex Formatter](https://latex-editor.pages.dev/formatter/)
2. [Latex formatter](https://latexformat.com)
3. [cmhughes/latexindent.pl](https://github.com/cmhughes/latexindent.pl)

#### 参考文献

1. [Google Scholar](https://scholar.google.com)
2. [ZoteroBib](https://zbib.org)
3. [Citation Machine](https://www.citationmachine.net)

### 模板和学习资源查询

#### 网站

1. [LaTeX](https://www.latex-project.org)
2. [LaTeX工作室](https://www.latexstudio.net)
3. [Overleaf Documentation](https://www.overleaf.com/learn)
4. [Overleaf Templates](https://www.overleaf.com/latex/templates)
5. [LaTeX Templates](https://www.latextemplates.com)
6. [MOON](https://www.moonpapers.com)
7. [BibTeX](https://www.bibtex.com)
8. [PGF/TikZ Manual](https://tikz.dev)
9. [TikZ](https://tikz.net)
10. [TeXample](https://texample.net)
11. [LaTeX Beamer](https://latex-beamer.com)

#### 教程

1. 各个宏包的说明文档（TeXstudio中在对应命令上右键打开）；
2. [latex中文教程-15集从入门到精通包含各种latex操作-bilibili](https://www.bilibili.com/video/BV15x411j7k6/)
3. [【1天玩转LaTeX】【写论文不怕格式出错啦！！！】【耿楠教授授权发布】-bilibili](https://www.bilibili.com/video/BV15b411j7Au/)
4. [LaTex教程【中文字幕】LaTeX by Michelle Krummel-bilibili](https://www.bilibili.com/video/BV1hK41157GG/)

#### GitHub

##### 教程

1. [CTeX-org/lshort-zh-cn](https://github.com/CTeX-org/lshort-zh-cn)
2. [MartinThoma/LaTeX-examples](https://github.com/MartinThoma/LaTeX-examples)
3. [wklchris/Note-by-LaTeX](https://github.com/wklchris/Note-by-LaTeX)
4. [egeerardyn/awesome-LaTeX](https://github.com/egeerardyn/awesome-LaTeX)
5. [xinychen/latex-cookbook](https://github.com/xinychen/latex-cookbook)
6. [huangxg/lnotes](https://github.com/huangxg/lnotes)
7. [tuna/thulib-latex-talk](https://github.com/tuna/thulib-latex-talk)
8. [oetiker/lshort](https://github.com/oetiker/lshort)
9. [OsbertWang/install-latex-guide-zh-cn](https://github.com/OsbertWang/install-latex-guide-zh-cn)
10. [wch/latexsheet](https://github.com/wch/latexsheet)
11. [xd15zhn/latexcookbook](https://github.com/xd15zhn/latexcookbook)

##### 模板

###### 文档模板

1. [ElegantLaTeX/ElegantBook](https://github.com/ElegantLaTeX/ElegantBook)
2. [ElegantLaTeX/ElegantPaper](https://github.com/ElegantLaTeX/ElegantPaper)
3. [ElegantLaTeX/ElegantNote](https://github.com/ElegantLaTeX/ElegantNote)
4. [DeathKing/LaTeX-Template-Cn](https://github.com/DeathKing/LaTeX-Template-Cn)
5. [kenfehling/latex-cheatsheet](https://github.com/kenfehling/latex-cheatsheet)
6. [sleepymalc/LaTeX-Template](https://github.com/sleepymalc/LaTeX-Template)
7. [LiuYongxue-code/Exam-USTC-demo](https://github.com/LiuYongxue-code/Exam-USTC-demo)

###### 简历模板

1. [posquit0/Awesome-CV](https://github.com/posquit0/Awesome-CV)
2. [billryan/resume](https://github.com/billryan/resume)
3. [sb2nov/resume](https://github.com/sb2nov/resume)
4. [dyweb/awesome-resume-for-chinese](https://github.com/dyweb/awesome-resume-for-chinese)
5. [jankapunkt/latexcv](https://github.com/jankapunkt/latexcv)
6. [hijiangtao/resume](https://github.com/hijiangtao/resume)
7. [darwiin/yaac-another-awesome-cv](https://github.com/darwiin/yaac-another-awesome-cv)
8. [huajh/awesome-latex-cv](https://github.com/huajh/awesome-latex-cv)
9. [dyweb/Deedy-Resume-for-Chinese](https://github.com/dyweb/Deedy-Resume-for-Chinese)

###### Beamer模板

1. [wzpan/BeamerStyleSlides](https://github.com/wzpan/BeamerStyleSlides)
2. [XiangyunHuang/awesome-beamers](https://github.com/XiangyunHuang/awesome-beamers)
3. [清华大学中文Beamer模板-Overleaf](https://www.overleaf.com/latex/templates/qing-hua-da-xue-zhong-wen-beamer-mo-ban/djcnhxpwhrks)
4. [TsinghuaBeamer-Overleaf](https://www.overleaf.com/latex/templates/tsinghuabeamer/gwchbskgbvrm)
5. [Trinkle23897/THU-Beamer-Theme](https://github.com/Trinkle23897/THU-Beamer-Theme)
6. [YangLaTeX/thubeamer](https://github.com/YangLaTeX/thubeamer)
7. [fuujiro/DLUT-Beamer-Slide-V2](https://github.com/fuujiro/DLUT-Beamer-Slide-V2)
8. [fuujiro/DLUT-Beamer-Slide-V1](https://github.com/fuujiro/DLUT-Beamer-Slide-V1)

###### 有趣模板

1. [Wandmalfarbe/pandoc-latex-template](https://github.com/Wandmalfarbe/pandoc-latex-template)
2. [Keldos-Li/typora-latex-theme](https://github.com/Keldos-Li/typora-latex-theme)
3. [MattX/texword](https://github.com/MattX/texword)

###### 基金申请模板

1. [Ruzim/NSFC-application-template-latex](https://github.com/Ruzim/NSFC-application-template-latex)
2. [Ruzim/NSFDYS-application-template](https://github.com/Ruzim/NSFDYS-application-template)
3. [MCG-NKU/NSFC-LaTex](https://github.com/MCG-NKU/NSFC-LaTex)
4. [YimianDai/iNSFC](https://github.com/YimianDai/iNSFC)
5. [huangwb8/ChineseResearchLaTeX](https://github.com/huangwb8/ChineseResearchLaTeX)
6. [fylimas/nsfc](https://github.com/fylimas/nsfc)

###### 高质量模板

1. [CS310-Assignment Template](https://www.overleaf.com/latex/templates/cs310-assignment-template/qrqpndrxpcht)
2. [Cheatsheet](https://www.latextemplates.com/template/cheatsheet)
3. [zheyuye/resume-chinese](https://github.com/zheyuye/resume-chinese)
4. [tuna/thuthesis](https://github.com/tuna/thuthesis)
5. [Academic Title Page](https://www.latextemplates.com/template/academic-title-page)

## 参考

1. [有没有LaTeX“编程”规范？-甚远的回答-知乎](https://www.zhihu.com/question/8239276228/answer/103448004359)
2. [!TeX-Stack Exchange](https://tex.stackexchange.com/questions/78101/when-and-why-should-i-use-tex-ts-program-and-tex-encoding)
3. [argmin&argmax-CSDN博客](https://blog.csdn.net/SunshineSki/article/details/87893347)
4. [矩阵转置-知乎](https://zhuanlan.zhihu.com/p/27490955)
5. [\prime-CSDN博客](https://blog.csdn.net/yq_forever/article/details/109029875)
6. [\triangleq-CSDN博客](https://blog.csdn.net/weixin_44550010/article/details/107864090)
7. [\overline-Stack Exchange](https://tex.stackexchange.com/questions/408084/how-to-place-a-wide-bar-over-a-wide-expression)
8. [公式上方下方大括号-百度经验](https://jingyan.baidu.com/article/020278118866ee1bcd9ce543.html)
9. [长竖线-知乎](https://www.zhihu.com/question/35119859/answer/61268787)
10. [\tab-Stack Exchange](https://tex.stackexchange.com/questions/198432/using-the-tab-command)
11. [对号&错号-Stack Exchange](https://tex.stackexchange.com/questions/42619/x-mark-to-match-checkmark)
12. [LaTeX页面设置-冬日暖阳的文章-知乎](https://zhuanlan.zhihu.com/p/360188228)
13. [空格-Stack Exchange](https://tex.stackexchange.com/questions/31091/space-after-latex-commands)
14. [音调1-CSDN博客](https://blog.csdn.net/xin_yu_xin/article/details/26467751)
15. [音调2-知乎](https://zhuanlan.zhihu.com/p/75828544)
16. [音调3-CSDN博客](https://blog.csdn.net/jianti9962/article/details/114481366)
17. [自定义命令1-Stack Exchange](https://tex.stackexchange.com/questions/36175/what-do-newcommand-renewcommand-and-providecommand-do-and-how-do-they-differ)
18. [自定义命令2-Stack Exchange](https://tex.stackexchange.com/questions/1050/whats-the-difference-between-newcommand-and-newcommand)
19. [字体大小-简书](https://www.jianshu.com/p/ad400d7fe885)
20. [列表-CSDN博客](https://blog.csdn.net/HugoChen_cs/article/details/105189541)
21. [公式1-简书](https://www.jianshu.com/p/97ec8a3739f6)
22. [公式2-CSDN博客](https://blog.csdn.net/Strive_For_Future/article/details/118609968)
23. [矩阵-知乎](https://zhuanlan.zhihu.com/p/266267223)
24. [图片1-CSDN博客](https://blog.csdn.net/qq_38526623/article/details/103737589)
25. [图片2-CSDN博客](https://blog.csdn.net/LeonSUST/article/details/89332744)
26. [单元格换行-CSDN博客](https://blog.csdn.net/robertchenguangzhi/article/details/48916319)
27. [\cline-CSDN博客](https://blog.csdn.net/huancaoo/article/details/113106636)
28. [\rule-Stack Exchange](https://tex.stackexchange.com/questions/50352/inserting-a-small-vertical-space-in-a-table)
29. [长度单位-CSDN博客](https://blog.csdn.net/robert_chen1988/article/details/52739825)
30. [\multirow-CSDN博客](https://blog.csdn.net/robert_chen1988/article/details/80861246)
31. [超链接-CSDN博客](https://blog.csdn.net/OOFFrankDura/article/details/90600855)
32. [代码块1-Overleaf](https://www.overleaf.com/learn/latex/Code_listing)
33. [代码块2-CSDN博客](https://blog.csdn.net/RobertChenGuangzhi/article/details/45126785)
34. [脚注-LaTeX工作室](https://www.latexstudio.net/archives/51620.html)
35. [参考文献1-知乎](https://zhuanlan.zhihu.com/p/265479955)
36. [参考文献2-知乎](https://zhuanlan.zhihu.com/p/114733612)
37. [参考文献3-Stack Exchange](https://tex.stackexchange.com/questions/99615/backref-package-for-page-reference)
38. [参考文献4-CSDN博客](https://blog.csdn.net/xovee/article/details/109715706)
39. [参考文献5-CSDN博客](https://blog.csdn.net/xovee/article/details/109896563)
40. [LaTeX写作工具-平凡的文章-知乎](https://zhuanlan.zhihu.com/p/362505439)
41. [LaTeX公式转Word公式-简书](https://www.jianshu.com/p/0947ebcfc42e)
42. [截至目前LaTeX入门最好资料-我是科研小秘书的文章-知乎](https://zhuanlan.zhihu.com/p/585513318)
43. [Latex简明速查手册(8页)-磁悬浮青蛙呱呱呱的文章-知乎](https://zhuanlan.zhihu.com/p/508559139)
44. [如何用latex出数学卷子?-科研就会一点点的回答-知乎](https://www.zhihu.com/question/402111484/answer/3302539544)
45. [国家自然科学基金的LaTeX模板-bensz的文章-知乎](https://zhuanlan.zhihu.com/p/682230693)
46. [为什么国家自然科学基金申请没有latex模板？-暗影猪的回答-知乎](https://www.zhihu.com/question/377854398/answer/2826599575)
47. [为什么国家自然科学基金申请没有latex模板？-程明明的回答-知乎](https://www.zhihu.com/question/377854398/answer/96596638902)
