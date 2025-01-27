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

1. 在VS Code中配置Git扩展的`Git: Path`选项，在`settings.json`文件中指定Git可执行文件的路径和文件名：

    ```json
    "git.path": "D:\\Program Files\\Git\\bin\\git.exe"
    ```

2. 在终端仿真器中配置字符编码为UTF-8，防止中文显示乱码：

    ```shell
    git config --global core.quotepath false            # 设置不转义特殊字符，文件路径不用编码模式显示
    git config --global gui.encoding utf-8              # 图形界面编码
    git config --global i18n.commit.encoding utf-8      # 提交信息编码
    git config --global i18n.logoutputencoding utf-8    # 输出log编码
    export LESSCHARSET=utf-8                            # less命令编码，输出log默认使用less命令分页
    ```

#### 使用

1. 安装并配置Git后可以在VS Code中使用Git的全部功能；
2. 可以在Git Bash终端仿真器中使用Git的命令行操作；

## Ubuntu

使用VS Code，其UI已经集成Git命令，结合GitHub相关扩展进行管理。

1. 设置Git用户名和邮箱：

    - 系统设置，所有系统用户的设置，保存在`/etc/gitconfig`文件中，极少使用，优先级最低；
    - 全局设置，当前系统用户的设置，保存在`~/.gitconfig`文件中，优先级中等：

        ```shell
        git config --global user.name "your name"
        git config --global user.email "your@email.com"
        git config --global -l  # 列出所有全局设置
        ```

    - 本地设置，当前仓库的设置，保存在`.git/config`文件中，优先级最高：

        ```shell
        git config --local user.name "your name"
        git config --local user.email "your@email.com"
        git config --local -l   # 列出所有本地设置
        ```

    - 更改全局设置前需要删除`~/.ssh/id_rsa`以及`~/.ssh/id_rsa.pub`；
    - 设置的邮箱需要添加到GitHub账号中才能计算贡献；

2. 创建SSH key：

    ```shell
    ssh-keygen -t rsa -b 2048 -C "your@email.com"
    ```

    - 连续点三次回车确认；
    - 美国国家标准与技术研究院（National Institute of Standards and Technology，NIST）建议使用至少2048位的SSH key；

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

7. 使用HTTPS进行git clone和git push时仍需要使用用户名和密码，**自2021年8月14日起，GitHub取消了在命令行内使用用户名和密码的clone方式，改为使用个人访问令牌（Personal Access Token，PAT），其作用和使用方式与密码相同：**

    ```shell
    git clone https://github.com/<username>/<repository>.git
    ```

8. 及时删除不再使用的SSH key以及PAT；

## GitHub

1. `Contribution settings`->勾选`Private contributions`
2. `Settings`->`Emails`->勾选`Keep my email addresses private`；
3. PAT的生成和使用：

    - `Settings`->`Developer settings`->`Personal access tokens`->`Generate new token`；
    - 设置token名称、有效期，有效范围（勾选`repo`）；
    - 点击`Generate token`，将生成的token保存；

4. 双因素身份校验（Two-Factor Authentication，2FA）的设置和使用，**自2023年10月6日起，在登录GitHub时需要使用2FA**：

    - `Settings`->`Password and authentication`->`Two-factor authentication`；
    - 使用神锁离线版扫描二维码，保存秘钥，用于生成基于时间的一次性密码（Time-based One-Time Password，TOTP）；
    - 在登录GitHub时除了需要使用账号密码，还需要使用根据秘钥和当前时间生成的一次性密码（One-Time Password，OTP），OTP每30秒动态更新一次；
    - 保存恢复码（recovery codes），用于在丢失密码和秘钥时登录GitHub，否则会永远丢失账号；
    - 也可以使用短信验证的方式进行2FA，但是目前暂时不支持中国大陆；

## 参考

1. [GitHub Desktop](https://desktop.github.com)
2. [desktop/desktop](https://github.com/desktop/desktop)
3. [Git](https://git-scm.com)
4. [git/git](https://github.com/git/git)
5. [Git for Windows](https://gitforwindows.org)
6. [git-for-windows/git](https://github.com/git-for-windows/git)
7. [Differences between Git-scm, msysGit & Git for Windows-Stack Overflow](https://stackoverflow.com/questions/22310007/differences-between-git-scm-msysgit-git-for-windows)
8. [Windows系统Git安装教程（详解Git安装过程）-maanlong的文章-知乎](https://zhuanlan.zhihu.com/p/242540359)
9. [git显示中文和解决中文乱码-YuSoLi的文章-知乎](https://zhuanlan.zhihu.com/p/133706032)
10. [解决Git在windows下中文乱码的问题-小明同学的文章-知乎](https://zhuanlan.zhihu.com/p/357002483)
11. [Git客户端设置Windows下的字符编码-华为云](https://support.huaweicloud.com/usermanual-codehub/devcloud_hlp_0954.html)
12. [在VScode上配置Git-浪晋的文章-知乎](https://zhuanlan.zhihu.com/p/31417255)
13. [git config的全局和本地配置-chloneda的文章-知乎](https://zhuanlan.zhihu.com/p/121471974)
14. [git config的配置（system、global、local）](https://www.panyanbin.com/article/ff4e1f85.html)
15. [Recommendation for Key Management-NIST](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57Pt3r1.pdf)
16. [Missing contributions-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile)
17. [Managing email preferences-GitHub Docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences)
18. [Token authentication requirements for Git operations-GitHub Blog](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)
19. [Creating a personal access token-GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
20. [GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今天0点已执行-量子位的文章-知乎](https://zhuanlan.zhihu.com/p/399759963)
21. [GitHub强制要求开启两步验证了，但是1password要收费，怎么办？-游凯超的文章-知乎](https://zhuanlan.zhihu.com/p/615693483)
22. [GitHub要求2FA？不慌，有它帮你-神锁离线版的文章-知乎](https://zhuanlan.zhihu.com/p/512717901)
23. [开启GitHub的2FA-bilibili](https://www.bilibili.com/video/BV1sU4y1S7LA)
