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

我的$\LaTeX$使用笔记及格式约定，供个人速查使用。

<!-- more -->

## 常用宏包

```latex
\usepackage{amsmath,amsthm,amsfonts,amssymb,amscd}  % 数学公式、符号等宏包
\usepackage{enumerate}      % 插入带序号列表
\usepackage{graphicx}       % 插入图片
\usepackage{listings}       % 插入代码块

\usepackage{hyperref}       % 插入超链接
\usepackage[backref]{hyperref}      % 章节引回
\usepackage[pagebackref]{hyperref}  % 页码引回
\hypersetup{                % 超链接样式设置
    colorlinks=true,
    linkcolor=blue,
    linkbordercolor={0 0 1}
}
\hypersetup{hidelinks}      % 不显示超链接线框

\usepackage{ctex}           % 中文支持
\usepackage{mathtools}      % 插入分段函数

\usepackage{algorithm}      % 插入伪代码
\usepackage{algpseudocode}  % 插入伪代码
\renewcommand{\algorithmicrequire}{\textbf{Input:}} % Use Input in the format of Algorithm
\renewcommand{\algorithmicensure}{\textbf{Output:}} % Use Output in the format of Algorithm

\usepackage[framed,numbered,autolinebreaks,useliterate]{mcode}  % 插入MATLAB代码块，基于listings开发
\usepackage{multirow}       % 跨多行表格
\usepackage{subfigure}      % 插入子图

\usepackage{tabto}          % 插入Tab
\NumTabs{8}                 % define 8 equally spaced tabs starting at the left margin
                            % and spanning \linewidth

\usepackage{fontawesome}    % 添加小图标

\usepackage{pifont}         % 添加对号、错号
\newcommand{\cmark}{\ding{51}}  % 对号
\newcommand{\xmark}{\ding{55}}  % 错号
```

## 格式约定

1. 源码在遇到`\begin{}`时要缩进；
2. 数学符号参考[常用数学符号的 LaTeX 表示方法](https://mohu.org/info/symbols/symbols.htm)，但有以下几点注意事项：

    - 上下标使用`{}`括起来；
    - 矩阵和向量使用`\mathbf{}`或`\boldsymbol{}`；
    - 集合使用`\mathbb{}`；
    - 范数使用`\|`；
    - argmin使用`\mathop{\arg\min}\limits_{}`，argmax同理；
    - 小空格用`\quad`，大空格用`\qquad`；
    - 分式尽量使用`\dfrac{}{}`，若显示有问题再使用`\frac{}{}`；

3. 括号大小自动调整；

    ```latex
    \left(  \right)
    \left[  \right]
    \left{  \right}
    \left\| \right\|
    ```

4. 使用`\hfill`进行水平填充，同理，使用`\vfill`进行垂直填充；
5. 使用`\hspace{}`插入水平间隔，同理，使用`\vspace{}`插入垂直间隔，大括号前添加`*`表示强制插入；
6. 使用`\tab`插入`Tab`；
7. 公式、图片、表格的引用标记要进行区分：

    ```latex
    \label{eq:XXX}  % 公式
    \label{fig:XXX} % 图片
    \label{tab:XXX} % 表格
    ```

8. 插入对号、错号：

    ```latex
    \ding{51} % 对号
    \ding{55} % 错号
    ```

9. 使用`\today`插入当天日期；

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

```latex
\begin{align}
    \label{eq:1.2}
    & 公式内容 \\
    \label{eq:1.3}
    & 公式内容
\end{align}
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

```latex
\begin{dcases}
    公式内容 & 条件 \\
    公式内容 & 条件
\end{dcases}
```

1. `dcases`     条件为纯公式，文本使用`\text{}`；
2. `dcases*`    条件为纯文本，公式使用`$ $`；

#### 向量/矩阵

```latex
\begin{array}{ccc} % 指定每列的对齐方式，个数对应列数
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1 \\
\end{array}
```

1. 对齐方式：
    - c：center，居中；
    - l：left，左对齐；
    - r：right，右对齐；
2. 列之间可以添加分隔线`|`；

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
    - h：here，当前位置；
    - t：top，顶部；
    - b：bottom，底部；
    - p：page of its own，浮动页；
2. 强制浮动格式：`[!h]`，不考虑美观性；
3. 图片格式推荐`.eps`；
4. 图片跨双栏使用`\begin{figure*}`；

### 插入子图

以四个子图2*2排列为例进行说明。

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
    \centering
    \caption{Table Title} % 表格标题
    \label{tab:1}
    \begin{tabular}{ccc} % 指定每列的对齐方式，个数对应列数
        \hline
        方法 & APE [m] & RPE [%]\\
        \hline
        方法1 & 0.10 & 0.20 \\
        方法2 & 0.05 & 0.15 \\
        \hline
    \end{tabular}
\end{table}
```

1. 浮动格式说明同上；
2. 对齐方式说明同上；
3. 表格框线：
    - 水平框线：使用`\hline`；
    - 垂直框线：在列之间添加分隔线`|`；
4. 表格跨双栏使用`\begin{table*}`；
5. 不规则形状表格：

    ```latex
    \multicolumn{number of cols}{pos}{text} % 跨多列
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

TODO

## 代码块

```latex
\begin{lstlisting}
    代码段
\end{lstlisting}
```

TODO：显示样式设置

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
    author = {作者, 多个作者用 and 连接},
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

    - plain，按字母的顺序排列，比较次序为作者、年度和标题；
    - unsrt，样式同plain，只是按照引用的先后排序；
    - alpha，用作者名首字母+年份后两位作标号，以字母顺序排序；
    - abbrv，类似plain，将月份全拼改为缩写，更显紧凑；
    - ieeetr，国际电气电子工程师协会期刊样式；
    - acm，美国计算机学会期刊样式；
    - siam，美国工业和应用数学学会期刊样式；
    - apalike，美国心理学学会期刊样式；

#### 文献引用

```latex
\cite{name1}
\cite{name1, name2}
```

## 绘图

TODO

### 转换工具

1. [matlab2tikz/matlab2tikz](https://github.com/matlab2tikz/matlab2tikz)
2. [nschloe/tikzplotlib](https://github.com/nschloe/tikzplotlib)

## Beamer

TODO

## 高质量网站存档

### 提升输入效率

1. [常用数学符号的LaTeX表示方法](https://mohu.org/info/symbols/symbols.htm)
2. [Detexify](http://detexify.kirelabs.org/classify.html)
3. [公式王](https://gongshi.wang/)
4. [Tables Generator](https://www.tablesgenerator.com/)
5. [wch/latexsheet](https://github.com/wch/latexsheet)
6. [LaTeX在线：吴文中数学公式编辑器](https://latex.91maths.com/)
7. [blaisewang/img2latex-mathpix](https://github.com/blaisewang/img2latex-mathpix)

### 模板和学习资源

1. [LaTeX工作室](https://www.latexstudio.net/)
2. [Overleaf Templates](https://www.overleaf.com/latex/templates)
3. [LaTeX Templates](https://www.latextemplates.com)
4. [MOON](https://www.moonpapers.com/)

### 优质模板

1. [CS310-Assignment Template](https://www.overleaf.com/latex/templates/cs310-assignment-template/qrqpndrxpcht)
2. [Cheatsheet](https://www.latextemplates.com/template/cheatsheet)
3. [HarisIqbal88/PlotNeuralNet](https://github.com/HarisIqbal88/PlotNeuralNet)
4. [zheyuye/resume-chinese](https://github.com/zheyuye/resume-chinese)
5. [tuna/thuthesis](https://github.com/tuna/thuthesis)
6. [Academic Title Page](https://www.latextemplates.com/template/academic-title-page)

### 学校beamer模板

1. [清华大学中文Beamer模板](https://www.overleaf.com/latex/templates/qing-hua-da-xue-zhong-wen-beamer-mo-ban/djcnhxpwhrks)
2. [Trinkle23897/THU-Beamer-Theme](https://github.com/Trinkle23897/THU-Beamer-Theme)
3. [fuujiro/DLUT-Beamer-Slide-V2](https://github.com/fuujiro/DLUT-Beamer-Slide-V2)
4. [fuujiro/DLUT-Beamer-Slide-V1](https://github.com/fuujiro/DLUT-Beamer-Slide-V1)

### 有趣模板

1. [Keldos-Li/typora-latex-theme](https://github.com/Keldos-Li/typora-latex-theme)
2. [MattX/texword](https://github.com/MattX/texword)

## 参考

1. 各个宏包的说明文档（TeXstudio中在对应命令上右键打开）
2. [latex中文教程-15集从入门到精通包含各种latex操作-bilibili](https://www.bilibili.com/video/BV15x411j7k6)
3. [【1天玩转LaTeX】【写论文不怕格式出错啦！！！】【耿楠教授授权发布】-bilibili](https://www.bilibili.com/video/BV15b411j7Au)
4. [LaTex教程【中文字幕】LaTeX by Michelle Krummel-bilibili](https://www.bilibili.com/video/BV1hK41157GG)
5. [\tab-Stack Exchange](https://tex.stackexchange.com/questions/198432/using-the-tab-command)
6. [对号&错号-Stack Exchange](https://tex.stackexchange.com/questions/42619/x-mark-to-match-checkmark)
7. [列表-CSDN博客](https://blog.csdn.net/HugoChen_cs/article/details/105189541)
8. [公式-简书](https://www.jianshu.com/p/97ec8a3739f6)
9. [图片1-CSDN博客](https://blog.csdn.net/qq_38526623/article/details/103737589)
10. [图片2-CSDN博客](https://blog.csdn.net/LeonSUST/article/details/89332744)
11. [\multirow-CSDN博客](https://blog.csdn.net/robert_chen1988/article/details/80861246)
12. [超链接-CSDN博客](https://blog.csdn.net/OOFFrankDura/article/details/90600855)
13. [脚注-LaTeX 工作室](https://www.latexstudio.net/archives/51620.html)
14. [参考文献1-知乎](https://zhuanlan.zhihu.com/p/265479955)
15. [参考文献2-知乎](https://zhuanlan.zhihu.com/p/114733612)
16. [参考文献3-Stack Exchange](https://tex.stackexchange.com/questions/99615/backref-package-for-page-reference)
