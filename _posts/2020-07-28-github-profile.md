---
layout: post
title: GitHub Profile的配置
date: 2020-07-28
author: zxl19
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何配置GitHub Profile，在个人页中显示详细信息。

<!-- more -->

## 创建GitHub Profile

1. 新建仓库，仓库名与用户名一致；
2. 选择仓库属性为Public；
3. 勾选README初始化选项。

## 动态显示GitHub统计信息

添加以下语句以动态生成统计信息：

```html
<a href="https://github.com/zxl19">
  <img align="left" src="https://github-readme-stats.vercel.app/api?username=zxl19&count_private=true&show_icons=true&theme=prussian" />
</a>
<a href="https://github.com/zxl19">
  <img align="left" src="https://github-readme-stats.vercel.app/api/top-langs/?username=zxl19&layout=compact&theme=prussian" />
</a>
```

效果如下：

[![zxl19's GitHub Stats](https://github-readme-stats.vercel.app/api?username=zxl19&count_private=true&show_icons=true&theme=prussian)](https://github.com/zxl19)

[![zxl19's Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=zxl19&layout=compact&theme=prussian)](https://github.com/zxl19)

具体使用方式和配置详见[GitHub Readme Stats](https://github.com/anuraghazra/github-readme-stats)

## 生成项目标签

可以在[网站](https://shields.io/)上生成标签。

添加以下语句以生成项目标签，以[996.ICU](https://github.com/996icu/996.ICU)为例。

### 左对齐

```markdown
[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu) [![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)
```

效果如下：

[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu) [![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)

### 居中

```html
<p align="center">
    <a href="https://996.icu">
        <img src="https://img.shields.io/badge/link-996.icu-red.svg" alt="Badge" />
    </a>
    <a href="https://github.com/996icu/996.ICU/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Anti%20996-blue.svg" alt="LICENSE" />
    </a>
</p>
```

效果如下：

<p align="center">
    <a href="https://996.icu">
        <img src="https://img.shields.io/badge/link-996.icu-red.svg" alt="Badge" />
    </a>
    <a href="https://github.com/996icu/996.ICU/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Anti%20996-blue.svg" alt="LICENSE" />
    </a>
</p>

## 参考

1. [GitHub隐藏新功能！个人页还能这么玩？-GitHub Daily的文章-知乎](https://zhuanlan.zhihu.com/p/161029860)
2. [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
3. [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
4. [996icu/996.ICU](https://github.com/996icu/996.ICU)
5. [antonkomarev/github-profile-views-counter](https://github.com/antonkomarev/github-profile-views-counter)
6. [jwenjian/visitor-badge](https://github.com/jwenjian/visitor-badge)
7. [gjbae1212/hit-counter](https://github.com/gjbae1212/hit-counter)
