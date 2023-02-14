---
layout: post
title: 在Windows和Ubuntu系统中使用GitHub进行版本管理
date: 2020-06-25
author: zxl19
tags: [Git, GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Windows和Ubuntu系统中使用GitHub进行版本管理。

<!-- more -->

## Windows

### GitHub Desktop

GitHub Desktop是GitHub开发的客户端，使用图形化交互界面代替了Git的命令行操作，可以满足大部分需求，但是其内置的Git无法在编辑器中使用。

### Git for Windows

#### 安装

在[官网](https://git-scm.com/download/win)下载Git安装包`Git-2.39.1-64-bit.exe`并运行：

1. `Information`许可证信息；
2. `Select Destination Location`选择安装位置：`D:\Program Files\Git`；
3. `Select Components`选择安装组件：

    - 勾选`Additional icons`->`On the Desktop`；
    - 勾选`Add a Git Bash Profile to Windows Terminal`；
    - 其余选项保持默认；

4. `Select Star Menu Folder`选择开始菜单文件夹；
5. `Choosing the default editor used by Git`选择Git使用的默认编辑器：`Use Visual Studio Code as Git's default editor`；
6. `Adjusting the name of the initial branch in new repositories`调整新仓库初始分支名：`Let Git decide`（目前默认初始分支名为`master`，后续可能更改）；
7. `Adjusting your PATH environment`调整PATH环境变量：`Git from the command line and also from 3rd-party software`（推荐）；
8. `Choosing the SSH executable`选择SSH可执行文件：`Use bundled OpenSSH`；
9. `Choosing HTTPS transport backend`选择HTTPS传输后端：`Use the OpenSSL library`；
10. `Configuring the line ending conversions`配置行尾序列转换：`Checkout Windows-style, commit Unix-style like line endings`；
11. `Configuring the terminal emulator to use with Git Bash`配置Git Bash使用的终端仿真器：`Use MinTTY(the default terminal of MSYS2)`；
12. `Choose the default behavior of 'git pull'`选择`git pull`的默认行为：`Default(fast-forward or merge)`；
13. `Choose a credential helper`选择安全证书助手：`Git Credential Manager`；
14. `Configuring extra options`配置其他选项：`Enable file system caching`；
15. `Configuring experimental options`配置实验选项：保持默认，全不勾选；

#### 配置

在VS Code中配置Git扩展的`Git: Path`选项，在`settings.json`文件中指定Git可执行文件的路径和文件名：

```json
"git.path": "D:\\Program Files\\Git\\bin\\git.exe"
```

#### 使用

1. 安装并配置Git后可以在VS Code中使用Git的全部功能；
2. 可以在Git Bash终端模拟器中使用Git的命令行操作；

## Ubuntu

使用VS Code，其UI已经集成Git命令，结合GitHub相关扩展进行管理。

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

5. 安装相关VS Code扩展，首次使用需要在GitHub网站上进行验证，授权VS Code登录；

    - GitHub Pull Requests and Issues
    - GitLens——Git supercharged

6. 使用SSH进行git clone和git push时不需要使用用户名和密码：

    ```shell
    git clone git@github.com:<username>/<repository>.git
    ```

7. 使用HTTPS进行git clone和git push时仍需要使用用户名和密码，**自2021年8月14日起，GitHub取消了在命令行内使用用户名和密码的clone方式，改为使用personal access token（PAT），其作用和使用方式与密码相同：**

    ```shell
    git clone https://github.com/<username>/<repository>.git
    ```

8. 及时删除不再使用的SSH key以及PAT；

## GitHub

1. `Contribution settings`->勾选`Private contributions`
2. `Settings`->`Emails`->勾选`Keep my email addresses private`；
3. PAT的生成和使用：

    - `Settings`->`Developer Settings`->`Personal access tokens`->`Generate new token`；
    - 设置token名称、有效期，有效范围（勾选`repo`）；
    - 点击`Generate token`，将生成的token保存；

## 参考

1. [GitHub Desktop](https://desktop.github.com)
2. [desktop/desktop](https://github.com/desktop/desktop)
3. [Git](https://git-scm.com)
4. [git/git](https://github.com/git/git)
5. [Differences between Git-scm, msysGit & Git for Windows](https://cloudaffaire.com/faq/differences-between-git-scm-msysgit-git-for-windows/)
6. [Windows系统Git安装教程（详解Git安装过程）-maanlong的文章-知乎](https://zhuanlan.zhihu.com/p/242540359)
7. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
8. [Missing contributions-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile)
9. [Managing email preferences-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences)
10. [Token authentication requirements for Git operations-GitHub Blog](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)
11. [Creating a personal access token-GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
12. [GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今天0点已执行-量子位的文章-知乎](https://zhuanlan.zhihu.com/p/399759963)
