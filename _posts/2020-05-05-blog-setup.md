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

选择合适的博客模板可以实现更加复杂的博客功能并提高博客的美观性，具体可以在[Jekyll Themes](http://jekyllthemes.org)网站上进行选择。本博客使用[FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)模板进行搭建，具体使用方式参考模板教程，在此向原作者表示感谢。完成此步骤之后，可以实现基本的博客功能。

1. [academicpages/academicpages.github.io](https://github.com/academicpages/academicpages.github.io)
2. [RayeRen/acad-homepage.github.io](https://github.com/RayeRen/acad-homepage.github.io)
3. [gaowei-space/markdown-blog](https://github.com/gaowei-space/markdown-blog)
4. [FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)

### 选择开源协议

在仓库中新建`LICENSE`文件，GitHub会自动提示可供选择的开源协议，并提供[说明](https://choosealicense.com)以供参考。本博客模板使用MIT开源协议，MIT与BSD类似，但是比BSD协议更加宽松，是目前最少限制的协议，这个协议唯一的条件就是在修改后的代码或者发行包包含原作者的许可信息，适用于商业软件。**2023年2月18日，本博客改为使用CC-BY-SA-4.0（知识共享-署名-相同方式共享-4.0版）开源协议，这是一种适用于非软件的开源协议。**

1. [Licensing a repository-GitHub Docs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
2. [The Legal Side of Open Source](https://opensource.guide/legal/)
3. [Choose an open source license](https://choosealicense.com)
4. [Creative Commons license-Wikipedia](https://en.wikipedia.org/wiki/Creative_Commons_license)
5. [About The Licenses-Creative Commons](https://creativecommons.org/licenses/)

### 设置赞赏按钮

在仓库中`Settings`->`General`->`Features`->`Sponsorships`，设置赞赏按钮，会在`.github`文件夹中生成`FUNDING.yml`文件，按照文件内的提示进行设置即可。如果不想注册相关网站可以上传微信赞赏码[^1]，在文件中添加微信赞赏码的链接来代替。

<p align="center">
    <a href="https://zxl19.github.io">
        <img src="https://raw.githubusercontent.com/zxl19/zxl19.github.io/master/images/funding.png" alt="buy me a coffee" width="300">
    </a>
</p>

[^1]: 以我的赞赏码为例。

### 设置收藏夹图标

收藏夹图标（favicon）指的是在网页标签栏和书签中显示的小图标，使用[图标生成器](https://android-material-icon-generator.bitdroid.de)制作收藏夹图标[^2]，在`_config.yml`文件中设置。

<p align="center">
    <a href="https://zxl19.github.io">
        <img src="https://raw.githubusercontent.com/zxl19/zxl19.github.io/master/images/icon.png" alt="my favicon" width="50">
    </a>
</p>

[^2]: 以我的收藏夹图标为例。

1. [Simple Icons](https://simpleicons.org)
2. [Android Material Icon Generator](https://android-material-icon-generator.bitdroid.de)
3. [Favicon Generator](https://redketchup.io/favicon-generator)
4. [favicon.io](https://favicon.io)
5. [免费Favicon.ico图标在线生成器](https://www.logosc.cn/logo/favicon)
6. [图标制作大师](https://geticon.cn)
7. [在线制作ico图标](https://www.bitbug.net)

### 设置评论区组件

LOFFER模板自V0.5.0开始支持[utterances](https://utteranc.es)评论区组件，安装这个GitHub App后可以将博客评论映射到仓库Issue。

1. 脚本和配置选项说明，可以直接添加到博客模板中：

    ```javascript
    <script src="https://utteranc.es/client.js"
            repo="zxl19/zxl19.github.io"            // 仓库名称
            issue-term="title"                      // Issue标题格式
            label="comment"                         // Issue标签
            theme="github-light"                    // 评论区主题
            crossorigin="anonymous"                 // 跨域设置
            async>
    </script>
    ```

2. 在`_config.yml`文件中设置：

    ```yaml
    utteranc:
        repo: zxl19/zxl19.github.io
        issue-term: title
        label: comment
        theme: github-light
        crossorigin: anonymous
    ```

    `utterance.html`文件会读取`_config.yml`文件中的设置：

    ```javascript
    <script src="https://utteranc.es/client.js"
            repo="{{ site.utteranc.repo }}"
            // 博客模板在这里有笔误，应为site.utteranc.issue-term
            issue-term="{{ site.utteranc.issue-term | default: 'issue-term' }}"
            label="{{ site.utteranc.label | default: 'utteranc' }}"
            theme="{{ site.utteranc.theme | default: 'github-light' }}"
            crossorigin="{{ site.utteranc.crossorigin | default: 'anonymous' }}"
            async>
    </script>
    ```

### 设置访问统计工具

使用[ClustrMaps](https://clustrmaps.com)组件实时统计博客访问信息并进行可视化[^3]，需要注册账号，同一个账号支持管理多个网址的访问信息并支持单独调整显示样式，如果需要重置某个网址的访问信息统计，需要删除其对应的项目。

```html
<script type='text/javascript' id='clustrmaps' src='//cdn.clustrmaps.com/map_v2.js?cl=ffffff&w=300&t=tt&d=hibP75SF_WZXl_4j4ksPzYOneT4Qb5-laVZ2YVjfDdA'></script>
```

**2024年11月：RevolverMaps停止提供服务。**

[^3]: 以我的脚本为例。

1. [RevolverMaps](https://www.revolvermaps.com)
2. [ClustrMaps](https://clustrmaps.com)
3. [Free website hit counter](https://www.free-website-hit-counter.com)

### 设置搜索引擎优化

搜索引擎优化（Search Engine Optimization，SEO）的目的是为了提高博客在搜索结果中的排名，在搜索引擎中搜索博客地址：

```text
site:https://zxl19.github.io
```

如果搜索结果中包含博客内容，则说明博客已被搜索引擎收录。

1. [Google Search Console](https://search.google.com/search-console/about)
2. [XML-Sitemaps](https://www.xml-sitemaps.com)

### 设置自定义404页面

在`404.md`文件头部添加：

```markdown
---
permalink: /404.html
---
```

1. [Creating a custom 404 page for your GitHub Pages site-GitHub Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site)

## 博客模板使用说明及格式约定

1. `_posts`文件夹中的每个`.md`文件对应一篇文章，文件名格式为`year-month-day-url.md`，以本文为例进行说明：

    - `year-month-day`为文件创建日期，例如：`2020-05-05`；
    - `url`为文章对应的二级域名，建议使用文章主题词，一般为两个单词，最多不超过三个单词，例如：`blog-setup`；
    - 博客模板不会使用隐藏的`.md`文件生成网页，因此在文件名前加`.`可以将文件隐藏，进而将对应文章隐藏；

2. 文章头部格式约定，以本文为例进行说明：

    ```markdown
    ---
    layout: post
    title: 如何利用GitHub搭建个人主页
    date: 2020-05-05
    author: zxl19
    categories:
    tags: [Blog, GitHub, Note]
    comments: true
    toc: true
    pinned: false
    ---
    ```

    - `layout`：排版样式，文章为`post`，对应`_layouts`文件夹中的`post.html`文件；
    - `title`：博客中显示的标题；
    - `date`：博客中显示的日期：

        - 博客模板根据此处的日期对于文章进行排序；
        - 建议此处使用最近一次修改日期，文件名中使用创建日期；
        - 为了避免文章顺序频繁变化，约定此处使用文件创建日期；

    - `author`：作者，多个作者使用英文逗号隔开，不需要使用中括号括起来；
    - `categories`：含义尚不明；
    - `tags`：标签；

        - 按照字母顺序排列，数量上尽量精简；
        - 多个标签使用英文逗号隔开，使用中括号括起来；
        - 最后一个标签表示文章类型，目前分为以下三种：

            | 标签 | 文章类型 |
            | :------ | :------ |
            | `Archive` | 资料存档，不定期更新 |
            | `Blog` | 博客，与生活相关 |
            | `Note` | 学习笔记，不定期更新 |

    - `comments`：是否开放评论，默认开放；
    - `toc`：是否生成目录，默认生成；
    - `pinned`：是否置顶，默认不置顶；

        - 置顶文章会在博客首页顶端显示，应尽量减少置顶文章数量，使博客显示美观；
        - 约定将所有需要置顶的文章链接按照时间顺序添加到`2023-02-27-hall-of-fame.md`文件中，只将这篇文章置顶；

3. 文章正文格式约定：

    - 为了防止自动截取摘要失败，约定在文章第一段后添加手动截取摘要的标记`<!-- more -->`，将包含特殊符号、代码块、表格的部分放在标记之后；
    - 为了文章显示美观，约定文章中不使用一级标题`#`，从二级标题`##`开始使用；
    - 为了防止排版样式显示错误，在文章正文中避免使用`|`，约定使用汉字“|”（音：滚）代替；
    - 为了防止有序列表序号显示不连续，约定将代码段和表格缩进到有序列表中；

## 常见问题及解决方法

### 无法生成网站

仓库属性必须为`Public`，否则无法生成网站。如果仓库属性设置错误，需要修改仓库属性后`git commit`+`git push`一次才能恢复正常。

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
6. [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
7. [Favicon的使用方法与制作-UIhacker的文章-知乎](https://zhuanlan.zhihu.com/p/50613376)
8. [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons)
9. [Maddoc42/Android-Material-Icon-Generator](https://github.com/Maddoc42/Android-Material-Icon-Generator)
10. [Online Tools-RedKetchup](https://redketchup.io)
11. [RevolverMaps](https://www.revolvermaps.com)
12. [ClustrMaps](https://clustrmaps.com)
13. [Have you noticed a change to the website?-NoFakeNews](https://nofakenews.net/2024/11/15/have-you-noticed-a-change-to-the-website)
14. [网站访问统计小工具RevolverMaps无法用了——平替ClustrMaps-CSDN博客](https://blog.csdn.net/weixin_43835470/article/details/144537126)
15. [谷歌搜索到自己在github的个人博客](https://fgc346.github.io/2023/04/13/OwnSiteByGoogleSearch/)
16. [GitHub Pages documentation-GitHub Docs](https://docs.github.com/en/pages)
17. [【最新】解决Github网页上图片显示失败的问题-CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)
18. [如何制作个人学术主页？-知乎](https://www.zhihu.com/question/281476526)
