---
layout: post
title: Gerrit代码审查使用笔记
date: 2025-01-15
author: zxl19
tags: [Gerrit, Note]
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
# clone with commit-msg hook
# 需要审核
git push origin HEAD:refs/for/{branch}
# 不需要审核
git push origin HEAD:refs/for/{branch}%submit
```

## 参考

1. [16个好用的Code Review工具-奶盖的文章-知乎](https://zhuanlan.zhihu.com/p/103592147)
2. [Gerrit Code Review](https://www.gerritcodereview.com)
3. [GerritCodeReview/gerrit](https://github.com/GerritCodeReview/gerrit)
4. [Gerrit代码Review入门实战-Hong Jack的文章-知乎](https://zhuanlan.zhihu.com/p/21482554)
5. [Gerrit使用指南-小新快跑的文章-知乎](https://zhuanlan.zhihu.com/p/714447850)
6. [如何一句话证明：你在谷歌、亚麻、FB…等大厂待过？-九章算法的文章-知乎](https://zhuanlan.zhihu.com/p/79771262)
7. [LGTM? 那些迷之缩写-CSDN博客](https://blog.csdn.net/misayaaaaa/article/details/102684348)