---
layout: post
title: LaTeX使用笔记
date: 2021-03-29
author: zxl19
tags: [LaTeX]
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
\hypersetup{                % 超链接格式设置
    colorlinks=true,
    linkcolor=blue,
    linkbordercolor={0 0 1}
}

\usepackage{ctex}           % 中文支持
\usepackage{mathtools}      % 插入分段函数

\usepackage{algorithm}      % 插入伪代码
\usepackage{algpseudocode}  % 插入伪代码
\renewcommand{\algorithmicrequire}{\textbf{Input:}} % Use Input in the format of Algorithm
\renewcommand{\algorithmicensure}{\textbf{Output:}} % Use Output in the format of Algorithm

\usepackage[framed,numbered,autolinebreaks,useliterate]{mcode}  % 插入MATLAB代码块，基于listings开发
\usepackage{multirow}       % 跨多行表格
\usepackage{subfigure}      % 插入子图
```

## 格式约定

1. 源码在遇到`\begin{}`时要缩进；
2. 数学符号参考[常用数学符号的 LaTeX 表示方法](https://mohu.org/info/symbols/symbols.htm)，但有以下几点注意事项：

    - 上下标使用`{}`括起来；
    - 矩阵和向量使用`\mathbf{}`；
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
    \label{eq1.1} % 引用标记
    公式内容
\end{equation}
```

##### 多个公式

```latex
\begin{align}
    \label{eq1.2}
    & 公式内容 \\
    \label{eq1.3}
    & 公式内容
\end{align}
```

##### 公式引用

```latex
\eqref{eq1.1}   % 有括号
\ref{eq1.2}     % 无括号
```

#### 无编号

```latex
\begin{align*}
    & 公式内容 \\
    & 公式内容
\end{align*}
```

#### 分段函数

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
    \label{fig.1}
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
        \label{fig.2a}
    }
    \quad
    \subfigure[Subfigure Title 2]
    {
        \includegraphics[width=0.3\textwidth]{image2.png}
        \label{fig.2b}
    }
    % 这里换行

    \subfigure[Subfigure Title 3]
    {
        \includegraphics[width=0.3\textwidth]{image3.png}
        \label{fig.2c}
    }
    \quad
    \subfigure[Subfigure Title 4]
    {
        \includegraphics[width=0.3\textwidth]{image4.png}
        \label{fig.2d}
    }
    \caption{Title} % 总标题
    \label{fig.2}
\end{figure}
```

## 表格

```latex
\begin{table}[htbp] % 指定表格位置
    \centering
    \caption{Table Title} % 表格标题
    \label{table.1}
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

## 高质量网站存档

### 提升输入效率

1. [常用数学符号的 LaTeX 表示方法](https://mohu.org/info/symbols/symbols.htm)
2. [Detexify](http://detexify.kirelabs.org/classify.html)
3. [公式王](https://gongshi.wang/)
4. [Tables Generator](https://www.tablesgenerator.com/)

### 模板和学习资源

1. [LaTeX 工作室](https://www.latexstudio.net/)
2. [Overleaf Templates](https://www.overleaf.com/latex/templates)
3. [LaTeX Templates](https://www.latextemplates.com)
4. [MOON](https://www.moonpapers.com/)

### 优质模板

1. [CS310-Assignment Template](https://www.overleaf.com/latex/templates/cs310-assignment-template/qrqpndrxpcht)
2. [Cheatsheet](https://www.latextemplates.com/template/cheatsheet)
3. [PlotNeuralNet](https://github.com/HarisIqbal88/PlotNeuralNet)

## 参考

1. [CSDN博客](https://blog.csdn.net/HugoChen_cs/article/details/105189541)
2. [CSDN博客](https://blog.csdn.net/qq_38526623/article/details/103737589)
3. [CSDN博客](https://blog.csdn.net/LeonSUST/article/details/89332744)
4. [CSDN博客](https://blog.csdn.net/robert_chen1988/article/details/80861246)
5. [CSDN博客](https://blog.csdn.net/OOFFrankDura/article/details/90600855)
6. [MOON博客](https://www.moonpapers.com/blog/5f8502bc30a4195e92ccc6db)