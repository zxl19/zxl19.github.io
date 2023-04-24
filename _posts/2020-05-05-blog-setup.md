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

选择合适的博客模板可以实现更加复杂的博客功能并提高博客的美观性，具体可以在[Jekyll Themes](http://jekyllthemes.org)网站上进行选择。本博客使用[FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)模板进行搭建，具体使用方式按照补充说明后的模板教程，在此向原作者表示感谢。完成此步骤之后，可以实现基本的博客功能。

1. [academicpages/academicpages.github.io](https://github.com/academicpages/academicpages.github.io)
2. [FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)
3. [RayeRen/acad-homepage.github.io](https://github.com/RayeRen/acad-homepage.github.io)

### 选择开源协议

在仓库中新建`LICENSE`文件，GitHub会自动提示可供选择的开源协议，并提供[说明](https://choosealicense.com)以供参考。本博客模板使用MIT开源协议，MIT与BSD类似，但是比BSD协议更加宽松，是目前最少限制的协议，这个协议唯一的条件就是在修改后的代码或者发行包包含原作者的许可信息，适用于商业软件。**2023年2月18日，本博客改为使用CC-BY-SA-4.0（知识共享-署名-相同方式共享-4.0版）开源协议，这是一种适用于非软件的开源协议。**

1. [Licensing a repository-GitHub Docs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
2. [The Legal Side of Open Source](https://opensource.guide/legal/)
3. [Choose an open source license](https://choosealicense.com)
4. [Creative Commons license-Wikipedia](https://en.wikipedia.org/wiki/Creative_Commons_license)
5. [About The Licenses-Creative Commons](https://creativecommons.org/licenses/)

### 设置赞赏按钮

在仓库的`Settings->Features->Sponsorships`中进行设置，会在`.github`文件夹中生成`FUNDING.yml`文件，按照文件内的提示进行设置即可。如果不想注册相关网站可以上传微信赞赏码[^1]，在文件中添加微信赞赏码的链接来代替。

<p align="center">
    <a href="https://zxl19.github.io">
        <img src="https://raw.githubusercontent.com/zxl19/zxl19.github.io/master/images/funding.png" alt="buy me a coffee" width="300">
    </a>
</p>

[^1]: 以我的赞赏码为例。

### icon生成

使用[图标生成器](https://android-material-icon-generator.bitdroid.de)，自定义网页标签栏中显示的小图标。

1. [Simple Icons](https://simpleicons.org)
2. [Android Material Icon Generator](https://android-material-icon-generator.bitdroid.de)
3. [Favicon Generator](https://redketchup.io/favicon-generator)

## 常见问题及解决方法

### GitHub图片显示失败

1. 修改hosts文件，具体参考[CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)进行解决；
2. 科学上网；

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
4. [Open Source Guides](https://opensource.guide)
5. [github/choosealicense.com](https://github.com/github/choosealicense.com)
6. [【最新】解决Github网页上图片显示失败的问题-CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)
7. [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
8. [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons)
9. [Maddoc42/Android-Material-Icon-Generator](https://github.com/Maddoc42/Android-Material-Icon-Generator)
10. [Online Tools-RedKetchup](https://redketchup.io)
11. [如何制作个人学术主页？-知乎](https://www.zhihu.com/question/281476526)
