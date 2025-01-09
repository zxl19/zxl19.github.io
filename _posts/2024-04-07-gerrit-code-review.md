---
layout: post
title: Gerrit代码审查使用笔记
date: 2024-04-07
author: zxl19
tags: [Gerrit, Archive]
comments: true
toc: true
pinned: false
---

我的Gerrit代码审查使用笔记。

<!-- more -->

```text
LGTM: Looks Good To Me
```

## Gerrit

```shell
# Clone with commit-msg hook
# 需要审核
git push origin HEAD:refs/for/master
git push origin HEAD:refs/for/refs/heads/master
# 不需要审核
git push origin HEAD:refs/for/master%submit
git push origin HEAD:master
git push origin HEAD:refs/heads/master
```

## 参考

1. [16个好用的Code Review工具-奶盖的文章-知乎](https://zhuanlan.zhihu.com/p/103592147)
2. [Gerrit Code Review](https://www.gerritcodereview.com)
3. [GerritCodeReview/gerrit](https://github.com/GerritCodeReview/gerrit)
4. [code review: gerrit实战-董姐姐的文章-知乎](https://zhuanlan.zhihu.com/p/69311610)
5. [Gerrit代码Review入门实战-Hong Jack的文章-知乎](https://zhuanlan.zhihu.com/p/21482554)
6. [如何一句话证明：你在谷歌、亚麻、FB…等大厂待过？-九章算法的文章-知乎](https://zhuanlan.zhihu.com/p/79771262)
7. [LGTM? 那些迷之缩写-CSDN博客](https://blog.csdn.net/misayaaaaa/article/details/102684348)
