---
layout: post
title: 在Windows和Ubuntu系统中使用GitHub进行版本管理
date: 2020-06-25
author: zxl19
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统中使用GitHub进行版本管理。

<!-- more -->

## Windows

使用GitHub Desktop进行管理，可以满足大部分需求。

## Ubuntu

使用VS Code，其UI已经集成Git命令，结合GitHub相关插件进行管理。

1. 设置Git全局变量：

    ```shell
    git config --global user.name "your name"
    git config --global user.email "your@email.com"
    ```

    - 更改之前设置的Git全局变量前需要删除`~/.ssh/id_rsa`以及`~/.ssh/id_rsa.pub`；
    - 设置的邮箱需要添加到GitHub账户中才能计算贡献；

2. 创建SSH key：

    ```shell
    ssh-keygen -t rsa -C "your@email.com"
    ```

    连续点三次回车确认。

3. 保存SSH key：

    复制`~/.ssh/id_rsa.pub`中的内容，在GitHub中`Setting`->`SSH and GPG keys`->`New SSH key`添加新的SSH key。

4. 完成通信设置：

    ```shell
    ssh -T git@github.com
    ```

    输入`yes`确认。

5. 首次使用需要在GitHub网站上进行验证，授权VS Code登录；
6. 安装相关VS Code插件；

    - GitHub Pull Requests and Issues
    - GitLens——Git supercharged

7. 使用SSH进行git clone和git push时不需要使用用户名和密码：

    ```shell
    git clone git@github.com:<username>/<repository>.git
    ```

8. 使用HTTPS进行git clone和git push时仍需要使用用户名和密码，**自2021年8月14日起，GitHub取消了在命令行内使用用户名和密码的clone方式，改为使用personal access token（PAT），其作用和使用方式与密码相同：**

    ```shell
    git clone https://github.com/<username>/<repository>.git
    ```

## GitHub

1. `Contribution settings`->勾选`Private contributions`
2. `Settings`->`Emails`->勾选`Keep my email addresses private`；
3. PAT的生成和使用：

    - `Settings`->`Developer Settings`->`Personal access tokens`->`Generate new token`；
    - 设置token名称、有效期，有效范围（勾选`repo`）；
    - 点击`Generate token`，将生成的token保存；

## 参考

1. [GitHub Desktop](https://desktop.github.com/)
2. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
3. [Missing contributions-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile)
4. [Managing email preferences-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences)
5. [Token authentication requirements for Git operations-GitHub Blog](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)
6. [Creating a personal access token-GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
7. [GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今天0点已执行-量子位的文章-知乎](https://zhuanlan.zhihu.com/p/399759963)
