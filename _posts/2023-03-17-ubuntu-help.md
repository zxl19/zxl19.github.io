---
layout: post
title: 在Ubuntu系统中查看命令帮助
date: 2023-03-17
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中查看命令帮助。

<!-- more -->

## 使用`-h`或`--help`选项

大部分命令都支持`-h`或`--help`选项，用于显示命令帮助。

## 使用`man`命令

1. `man`命令是系统自带的手册查询工具（manual pager），用于查询程序或函数的帮助手册页面；
2. 全部帮助手册页面可在[Manned.org](https://manned.org)上查看；
3. 语法说明：

    ```shell
    man [OPTION...] [SECTION] PAGE...
    ```

## 使用`tldr`命令

1. `tldr`命令是社区维护的命令行工具帮助页面查询工具；
2. 名称来源于互联网俚语“太长不看”（Too Long; Didn't Read，TL;DR）；
3. 语法说明：

    ```shell
    tldr command [options]
    ```

### 安装及配置

#### 安装

```shell
python3 -m pip install tldr
```

#### 配置

1. 在`~/.bashrc`文件或者是`~/.zshrc`文件中配置环境变量：

    ```shell
    export TLDR_COLOR_NAME="cyan"
    export TLDR_COLOR_DESCRIPTION="white"
    export TLDR_COLOR_EXAMPLE="green"
    export TLDR_COLOR_COMMAND="red"
    export TLDR_COLOR_PARAMETER="white"
    export TLDR_LANGUAGE="en"
    export TLDR_CACHE_ENABLED=1
    export TLDR_CACHE_MAX_AGE=720
    export TLDR_PAGES_SOURCE_LOCATION="https://raw.githubusercontent.com/tldr-pages/tldr/main/pages"
    export TLDR_DOWNLOAD_CACHE_LOCATION="https://tldr-pages.github.io/assets/tldr.zip"
    ```

2. 更新本地缓存，需要连接GitHub：

    ```shell
    tldr -u
    ```

3. 设置自动补全

    ```shell
    # bash
    tldr --print-completion bash | sudo tee "$BASH_COMPLETION_COMPAT_DIR"/tldr
    # zsh (it is recommended to check where zsh/site-functions directory is located)
    ## for Linux:
    tldr --print-completion zsh | sudo tee /usr/share/zsh/site-functions/_tldr
    ```

## 使用速查表

### 网站

1. [Cheat Sheet](https://cheat-sheets.org)
2. [Devhints](https://devhints.io)
3. [CheatSheets.zip](https://cheatsheets.zip)
4. [Quick Reference](https://wangchujiang.com/reference/)
5. [Linux命令搜索引擎](https://wangchujiang.com/linux-command/)
6. [鸟哥Linux命令大全](https://man.niaoge.com)
7. [cheat.sh](https://cheat.sh)
8. [bropages](http://bropages.org)

### GitHub

1. [tldr-pages/tldr](https://github.com/tldr-pages/tldr)
2. [tldr-pages/tldr-python-client](https://github.com/tldr-pages/tldr-python-client)
3. [jaywcjlove/linux-command](https://github.com/jaywcjlove/linux-command)
4. [denisidoro/navi](https://github.com/denisidoro/navi)
5. [rstacruz/cheatsheets](https://github.com/rstacruz/cheatsheets)
6. [cheat/cheat](https://github.com/cheat/cheat)
7. [jaywcjlove/reference](https://github.com/jaywcjlove/reference)
8. [Fechin/reference](https://github.com/Fechin/reference)
9. [gnebbia/kb](https://github.com/gnebbia/kb)
10. [srsudar/eg](https://github.com/srsudar/eg)
11. [darkmatter18/cheatsheet](https://github.com/darkmatter18/cheatsheet)
12. [Command Line Interface Pages](https://github.com/command-line-interface-pages)

## 参考

1. [Manned.org](https://manned.org)
2. [man page-Wikipedia](https://en.wikipedia.org/wiki/Man_page)
3. [Terminal pager-Wikipedia](https://en.wikipedia.org/wiki/Terminal_pager)
4. [哪些命令行工具让你相见恨晚？-程序员客栈的回答-知乎](https://www.zhihu.com/question/41115077/answer/602854935)
5. [tldr-pages/tldr](https://github.com/tldr-pages/tldr)
6. [tldr-pages/tldr-python-client](https://github.com/tldr-pages/tldr-python-client)
