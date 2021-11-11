---
layout: post
title: GitHub同步更新fork的项目
date: 2020-07-29
author: zxl19
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在GitHub中同步更新fork的项目。

<!-- more -->

## 操作步骤

1. 点击`Pull requests`；
2. 点击`New pull request`；
3. 左侧`base repository`和`base`选择自己的仓库和分支，右侧`head repository`和`compare`选择来源仓库和分支；
4. 点击`Create pull request`，填写创建信息；
5. 点击`Merge pull request`，自动检查冲突项；
6. 点击`Confirm merge`完成合并；

## 注意事项

在发生冲突无法合并的时候，需要按照说明通过命令行进行手动合并。

1. 首先将自己的仓库克隆到本地；
2. 按照GitHub上的第一步进行命令行操作：

    ```text
    Step 1: From your project repository, check out a new branch and test the changes.
    ```

    ```shell
    git checkout -b <new branch name> master
    git pull <original git repository> master
    ```

3. 按照提示修改冲突的文件，冲突在文件中以如下方式说明，手动修改保留对应部分：

    ```text
    <<<<<<< HEAD
    当前更改内容
    ======
    传入更改内容
    >>>>>>> id
    ```

4. 添加更改并提交：

    ```shell
    git add <filename>
    git commit -m "message"
    ```

5. 按照GitHub上的第二步进行命令行操作：

    ```text
    Step 2: Merge the changes and update on GitHub.
    ```

    ```shell
    git checkout master
    git merge --no-ff <new branch name>
    git push origin master
    ```

## 参考

1. [同步Fork-CSDN博客](https://blog.csdn.net/qq1332479771/article/details/56087333)
2. [Configuring a remote for a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork)
3. [Syncing a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
