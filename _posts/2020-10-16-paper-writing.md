---
layout: post
title: 不定期更新的论文写作注意事项
date: 2020-10-16
author: zxl19
tags: [Academic, Paper, Note]
comments: true
toc: true
pinned: false
---

这里是不定期更新的论文写作注意事项。

<!-- more -->

## 文章结构

1. 使用官方提供的模板；
2. 采用总-分结构，先综述本文的方法，然后介绍方法的各个部分，对于文章创新点对应的部分要着重介绍，最后通过实验说明：

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

### 整体原则

1. 图片中中文使用宋体，英文和数字使用Times New Roman；
2. 图片分辨率大于800像素；
3. 在使用Word时图片建议使用`.tiff`格式，更加清晰；
4. 在使用$\LaTeX$时图片格式建议首先使用`.pdf`格式，其次使用`.png`或`.jpg`格式，`.eps`格式已较少使用；
5. 指代图片时应使用图片编号，例如：“如图1所示”；
6. 在转换PDF时，使用`打印->打印机属性->印刷质量`提高图片的清晰度；

### 曲线图

1. 不同曲线之间线型和颜色都应存在区别，以保证论文在黑白打印下能够分辨不同曲线，如果实在无法区分，可在图名后添加如下说明：

    ```text
    (For colored figures, please refer to the online edition.)
    ```

2. 图片添加坐标轴名称、单位，不必在图中添加图名，可以在图名位置处添加简单说明；
3. MATLAB中设置图片大小示例：

    ```matlab
    set(gcf, 'Unit', 'Centimeters', 'Position', [10 5 15 10]) % 单个图像
    set(gcf, 'Unit', 'Centimeters', 'Position', [10 5 20 15]) % 三个子图
    ```

4. MATLAB中设置坐标轴字体示例：

    ```matlab
    set(gca, 'FontName', 'Times New Roman') % 子图中需要分别设置
    xlabel('\fontname{宋体}时间\fontname{Times New Roman} / s')
    ylabel('\fontname{Times New Roman}x / m')
    ```

5. 图片中的文字大小应保证与正文中的文字大小接近，建议使用固定字号18磅，搭配图片宽度15cm，$LaTeX$中`0.6\linewidth`；
6. 若不要求坐标轴比例相等可以放大坐标区充满图窗；
7. MATLAB中反转坐标轴方向示例：

    ```matlab
    set(gca, 'XDir', 'reverse')
    set(gca, 'YDir', 'reverse')
    ```

8. MATLAB中设置坐标轴刻度示例：

    ```matlab
    set(gca, 'XTick', [0 : 0.5 * pi : 2 * pi])
    set(gca, 'XTickLabel', {'0', '0.5\pi', '\pi', '1.5\pi', '2\pi'})
    ```

9. MATLAB中颜色图设置示例：

    ```matlab
    colormap default    % 默认颜色图设置，parula
    colormap jet        % 由蓝到红，较为美观
    colormap(jet)       % 作用相同
    ```

10. MATLAB中颜色栏设置示例：

    ```matlab
    c = colorbar;
    c.Label.String = '标注文字';
    ```

### 流程图和示意图

1. 流程图或简单插图使用`draw.io`绘制，通过网页版导出为`.pdf`；
2. 复杂插图使用PPT绘制，组合后另存为图片，优先选择`.png`格式，如果插图中部分元素显示存在黑色边框可以选择`.jpg`格式；

## 表格

1. 文章中提出的方法应做说明，效果好的方法应加粗显示；
2. Word中使用`分布列`保证列宽相同；

## 语言

1. 原则上少用被动语态，在主语未知、定语从句中或其它不可避免的情况下再使用；

## 审稿人意见回复

1. 参考[这个知乎问题](https://www.zhihu.com/question/370758333)进行回复；
2. 参考[这个B站视频](https://www.bilibili.com/video/BV1ix411o7qq)进行对线:dog:；

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

## 写作规范

1. [MLNLP-World/Paper-Writing-Tips](https://github.com/MLNLP-World/Paper-Writing-Tips)
2. [guanyingc/latex_paper_writing_tips](https://github.com/guanyingc/latex_paper_writing_tips)
3. [Haixing-Hu/typesetting-standard](https://github.com/Haixing-Hu/typesetting-standard)
4. [writing-resources/awesome-scientific-writing](https://github.com/writing-resources/awesome-scientific-writing)
5. [wangdongdut/PaperWriting](https://github.com/wangdongdut/PaperWriting)
6. [cooelf/PaperWritingTips](https://github.com/cooelf/PaperWritingTips)

### 英文写作

1. [正确写作美国大学生数学建模竞赛论文](https://github.com/RobbyDeng/MCM2019)
2. [English Exposed](https://hkupress.hku.hk/pro/con/1612.pdf)
3. [Academic Phrasebank](https://www.phrasebank.manchester.ac.uk/)
4. [The Most Common Habits from more than 200 English Papers written by Graduate Chinese Engineering Students](https://www.chrisyttang.org/assets/misc/The%20Most%20Common%20Habits%20from%20more%20than%20200%20English%20Papers%20written.pdf)

## 参考

1. [MATLAB画图字体-CSDN博客](https://blog.csdn.net/weixin_44891861/article/details/117032147)
2. [MATLAB坐标轴位置和方向设置-CSDN博客](https://blog.csdn.net/yuejisuo1948/article/details/80801506)
3. [MATLAB坐标轴刻度设置-百度经验](https://jingyan.baidu.com/article/c1a3101e044849de646deb43.html)
4. [MATLAB坐标轴刻度设置-CSDN博客](https://blog.csdn.net/yq_forever/article/details/86594602)
5. [审稿意见怎么回复？需要注意什么？-知乎](https://www.zhihu.com/question/370758333)
6. [英文论文写作有哪些需要注意的细节？-知乎](https://www.zhihu.com/question/46825717)
7. [我来分享下自己总结的审稿意见回复的模板吧-方差的文章-知乎](https://zhuanlan.zhihu.com/p/346911007)
8. [美国老姐看完200+中国学生SCI论文，怒写超详细“中国人英文论文写作指南”，还被推上了B站热门…-量子位的文章-知乎](https://zhuanlan.zhihu.com/p/512095069)
