---
layout: post
title: 在Windows和Ubuntu系统下使用GitHub进行版本管理
date: 2020-06-25
author: zxl19
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统下使用GitHub进行版本管理。

<!-- more -->

## Windows

使用GitHub Desktop进行管理，可以满足大部分需求。

## Ubuntu

**注：自2021年8月14日起，GitHub取消了在命令行内使用用户名和密码的clone方式，改为使用Personal access tokens，以下方法还有待检验和更新**

使用VS Code，UI已经集成git命令，结合插件进行管理。

1. 设置全局变量

    ```shell
    git config --global user.name "your name"
    git config --global user.email "your@email.com"
    ```

2. 创建SSH key

    ```shell
    ssh-keygen -t rsa -C "your@email.com"
    ```

    连续点三次回车确认。

3. 保存SSH key

    复制`~/.ssh/id_rsa.pub`中的内容，在GitHub中`Setting`->`SSH and GPG keys`->`New SSH key`添加新的SSH key。

4. 完成通信设置

    ```shell
    ssh -T git@github.com
    ```

    输入`yes`确认。

5. 首次使用需要在GitHub网站上进行验证，授权VS Code登录
6. 安装相关VS Code插件：
    - GitHub Pull Requests and Issues
    - GitLens——Git supercharged

## 参考

1. [GitHub Desktop](https://desktop.github.com/)
2. [GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今天0点已执行-量子位的文章-知乎](https://zhuanlan.zhihu.com/p/399759963)
3. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
4. [github/gitignore](https://github.com/github/gitignore)
