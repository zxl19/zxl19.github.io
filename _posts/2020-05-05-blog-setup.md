---
layout: post
title: 如何利用Github搭建个人主页
date: 2020-06-05
author: zxl19
tags: [blog]
comments: true
toc: true
pinned: true
---

如题，简单记录一下本博客的搭建过程。

## 搭建过程

### 选择模板
在[模板网站](http://jekyllthemes.org/)上进行选择，本博客采用[LOFFER模板](https://github.com/FromEndWorld/LOFFER)，具体使用方式详见README文档，在此向作者表示感谢。

注意一定不要将仓库建为Private。

<!-- more -->

### 选择开源协议
在仓库中新建LICENSE文件，Github会自动提示可供选择的开源协议，并提供[说明](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project)以供参考。本博客遵循MIT开源协议，MIT与BSD类似，但是比BSD协议更加宽松，是目前最少限制的协议，这个协议唯一的条件就是在修改后的代码或者发行包包含原作者的许可信息，适用于商业软件[^1]。

[^1]: 其实直接参考大神的仓库也是一个很好的方法。

### 设置赞赏按钮
在Setting中进行设置，按照教程进行设置，如果不想注册网站可以用[微信赞赏码](https://raw.githubusercontent.com/zxl19/zxl19.github.io/master/images/funding.png)[^2]代替。

[^2]: 点一下吧，秋梨膏！

### icon生成
使用[图标生成器](https://android-material-icon-generator.bitdroid.de/)

## 常见问题

### 解决Github图片显示的问题
参考[CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)进行解决。

### 将代码托管到Gitee上
可以参考[B站视频](https://www.bilibili.com/video/BV1cJ411h7q3)，尝试未成功。

### 另外一种简单的搭建教程
参考[知乎回答](https://www.zhihu.com/question/20962496/answer/677815713)，可以搭建一个简单的个人主页，作为简历使用比较合适，但是实现更加复杂的功能比较困难。

## 参考
1. [如何在GitHub上写博客？-少数派的回答-知乎](https://www.zhihu.com/question/20962496/answer/677815713)
2. [Gitee码云pages+Jekyll主题搭建个人博客](https://www.bilibili.com/video/BV1cJ411h7q3)
3. [各种开源协议介绍](https://www.runoob.com/w3cnote/open-source-license.html)
4. [【最新】解决Github网页上图片显示失败的问题](https://blog.csdn.net/qq_38232598/article/details/91346392)
5. [几条经验美化你的GitHub开源项目](https://www.jianshu.com/p/d587b91bacb3)