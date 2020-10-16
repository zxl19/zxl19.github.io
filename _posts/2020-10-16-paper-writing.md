---
layout: post
title: 论文写作注意事项
date: 2020-10-16
author: zxl19
tags: [Paper]
comments: true
toc: true
pinned: false
---

这里是不定期更新的论文写作注意事项。

<!-- more -->

## 文章结构

1. 使用官方提供的模板；
2. 采用总-分结构，先综述本文的方法，然后介绍方法的各个部分，最后通过实验说明；

    ```text
    Abstract
    Introduction
    Method Overview
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
4. 公式和编号右对齐，在中间用`Tab`键隔开。

## 图片

1. 导出`.tiff`格式的图片，更加清晰；
2. MATLAB中设置图片大小实例：

    ```MATLAB
    set(gcf,'Unit', 'Centimeters', 'Position', [10 5 15 13.5]);
    ```

3. 图片中的文字大小与正文中的文字大小接近。

## 表格

1. 文章中提出的方法应做说明，效果好的方法应加粗显示。

## 语言

1. 尽量少用被动语态。