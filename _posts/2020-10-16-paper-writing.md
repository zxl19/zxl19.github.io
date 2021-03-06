---
layout: post
title: 不定期更新的论文写作注意事项
date: 2020-10-16
author: zxl19
tags: [Paper, Note]
comments: true
toc: true
pinned: false
---

这里是不定期更新的论文写作注意事项。

<!-- more -->

## 文章结构

1. 使用官方提供的模板；
2. 采用总-分结构，先综述本文的方法，然后介绍方法的各个部分，对于文章创新点对应的部分要着重介绍，最后通过实验说明；

    ```text
    Abstract
    Introduction
    Related Works
    Methodology
    Experiments
    Conclusions
    References
    ```

    ```text
    Abstract
    Introduction
    Method Part1
    Method Part2
    Method Part3
    Experiments
    Summary/Conclusions
    Reference
    Contact Information
    Acknowledgements
    ```

3. 文字采用两端对齐更加美观；
4. 公式和编号右对齐，在中间用`Tab`键隔开；

## 图片

1. 不同曲线之间线型和颜色都应存在区别，以保证论文在黑白打印下能够分辨不同曲线，如果实在无法区分，可在图名后添加如下说明：

    ```text
    (For colored figures, please refer to the online edition.)
    ```

2. 图片添加坐标轴名称、单位，不必在图中添加图名，可以在图名位置处添加简单说明；
3. 导出图片格式建议使用`.tiff`，更加清晰，在使用$\LaTeX$时图片使用`.png`或者是`.eps`格式；
4. MATLAB中设置图片大小示例：

    ```matlab
    set(gcf,'Unit', 'Centimeters', 'Position', [10 5 15 13.5]);
    ```

5. 图片中的文字大小应保证与正文中的文字大小接近；
6. 流程图或简单插图使用`draw.io`绘制，复杂插图使用PPT绘制，组合后另存为图片；
7. 指代图片时应使用图片编号，例如：“如图1所示”；
8. 图片分辨率大于800像素；
9. 在转换PDF时，使用`打印->打印机属性->印刷质量`提高图片的清晰度；

## 表格

1. 文章中提出的方法应做说明，效果好的方法应加粗显示；
2. Word中使用`分布列`保证列宽相同；

## 语言

1. 原则上少用被动语态，在主语未知、定语从句中或其它不可避免的情况下再使用；

## 审稿人意见回复

1. 参考[知乎问题](https://www.zhihu.com/question/370758333)；
2. 参考[B站视频](https://www.bilibili.com/video/BV1ix411o7qq)进行对线 \doge；

## 作者信息

1. 用`*`上标表示通信作者（Corresponding author/Correspondence）；
2. 作者邮箱信息字体：

    ```latex
    \usepackage{courier}
    % 打字机字体/等宽字体
    \texttt{john_doe@xxx.xxx}
    ```

3. 通信作者邮箱加超链接；

## 资料

### 期刊目录

1. [中国计算机学会推荐国际学术会议和期刊目录](https://www.ccf.org.cn/c/2019-04-25/663625.shtml)
2. [汽车工程领域高质量科技期刊分级目录](http://m.sae-china.org/a4040.html)

### 英文写作

1. [正确写作美国大学生数学建模竞赛论文](https://github.com/RobbyDeng/MCM2019)
2. [English Exposed](https://hkupress.hku.hk/pro/con/1612.pdf)
3. [Academic Phrasebank](https://www.phrasebank.manchester.ac.uk/)

## 参考

1. [审稿意见怎么回复？需要注意什么？-知乎](https://www.zhihu.com/question/370758333)
2. [英文论文写作有哪些需要注意的细节？-知乎](https://www.zhihu.com/question/46825717)
