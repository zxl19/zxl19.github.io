---
layout: post
title: Github同步更新fork的项目
date: 2020-07-29
author: zxl19
tags: [GitHub]
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
6. 点击`Confirm merge`完成合并。

## 注意事项

在发生冲突无法合并的时候，需要按照说明通过命令行进行手动合并。

Step 1: From your project repository, check out a new branch and test the changes.

```shell
git checkout -b RobustFieldAutonomyLab-master master
git pull https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git master
```

Step 2: Merge the changes and update on GitHub.

```shell
git checkout master
git merge --no-ff RobustFieldAutonomyLab-master
git push origin master
```

## 参考

1. [CSDN博客](https://blog.csdn.net/qq1332479771/article/details/56087333)
2. [Configuring a remote for a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork)
3. [Syncing a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
