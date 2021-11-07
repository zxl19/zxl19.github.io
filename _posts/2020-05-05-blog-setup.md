---
layout: post
title: 如何利用GitHub搭建个人主页
date: 2020-05-05
author: zxl19
tags: [Blog, GitHub, Note]
comments: true
toc: true
pinned: false
---

如题，简单记录一下本博客的搭建过程。

<!-- more -->

## 搭建过程

### 选择博客模板

选择合适的博客模板可以实现更加复杂的博客功能并提高博客的美观性，具体可以在[基于Jekyll的模板网站](http://jekyllthemes.org/)上进行选择。本博客采用[LOFFER模板](https://github.com/FromEndWorld/LOFFER)，具体使用方式按照补充说明后的模板教程，在此向原作者表示感谢。完成此步骤之后，可以实现基本的博客功能。

### 选择开源协议

在仓库中新建LICENSE文件，GitHub会自动提示可供选择的开源协议，并提供[说明](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project)以供参考。本博客遵循MIT开源协议，MIT与BSD类似，但是比BSD协议更加宽松，是目前最少限制的协议，这个协议唯一的条件就是在修改后的代码或者发行包包含原作者的许可信息，适用于商业软件[^1]。

[^1]: 其实直接参考大神的仓库也是一个很好的方法。

### 设置赞赏按钮

在仓库的Settings->Features->Sponsorships中进行设置，会在.github文件夹中生成FUNDING.yml文件，按照文件内的提示进行设置即可。如果不想注册相关网站可以上传[微信赞赏码](https://raw.githubusercontent.com/zxl19/zxl19.github.io/master/images/funding.png)[^2]，在文件中添加微信赞赏码的链接来代替。

[^2]: 以我的赞赏码为例。

### icon生成

使用[图标生成器](https://android-material-icon-generator.bitdroid.de/)，自定义网页标签栏中显示的小图标。

## 常见问题

### GitHub图片显示失败

修改hosts文件，具体参考[CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)进行解决。

### 在Gitee上同步博客

在Gitee上也可以搭建个人主页，可以保证访问速度和稳定性，具体参考[B站视频](https://www.bilibili.com/video/BV1cJ411h7q3)。

曾尝试将本博客仓库托管到Gitee后同步搭建Gitee Pages，未成功。

### 另外一种简单的搭建教程

不使用博客模板新建仓库，搭建简单的GitHub Page，参考[知乎回答](https://www.zhihu.com/question/20962496/answer/677815713)，可以搭建一个简单的个人主页，可以作为项目介绍页或者简历使用，美观性较差，也难以实现更加复杂的功能。

### 博客模板更新同步

由于博客仓库通过博客模板构建，在博客模板更新后无法通过Pull Request的方式进行同步。为实现对于博客模板更新的同步，可以保留`_posts`文件夹下的文件，将其他文件直接替换为更新后博客模板中的文件，在进行简单配置后即可完成同步更新。

## 参考

1. [如何在GitHub上写博客？-少数派的回答-知乎](https://www.zhihu.com/question/20962496/answer/677815713)
2. [Gitee码云pages+Jekyll主题搭建个人博客-bilibili](https://www.bilibili.com/video/BV1cJ411h7q3)
3. [各种开源协议介绍-菜鸟教程](https://www.runoob.com/w3cnote/open-source-license.html)
4. [【最新】解决Github网页上图片显示失败的问题-CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)
5. [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
6. [如何制作个人学术主页？-知乎](https://www.zhihu.com/question/281476526)
