---
layout: post
title: 在Ubuntu系统中压缩、解压缩文件
date: TODO
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中压缩、解压缩文件。

<!-- more -->

## tar

### 选项说明

### 压缩

```shell
tar -cvf test.tar *.cpp
```

```shell
tar -czvf test.tar.gz *.cpp
```

### 解压缩

```shell
tar -xvf test.tar
```

```shell
tar -xzvf test.tar.gz
```

## zip

### 选项说明

```shell
zip test.zip *.cpp
zip -s 4000m test.zip --out part
```

```shell
cat part.z* > test.zip
unzip test.zip
```

## 7z

### 安装

```shell
sudo apt install p7zip-full
sudo apt install p7zip-rar
```

### 压缩

### 解压缩

## 参考

1. [Linux下的tar压缩解压缩命令详解-不懂球的胖子的文章-知乎](https://zhuanlan.zhihu.com/p/34841993)
2. [tar解压缩命令详解-博客园](https://www.cnblogs.com/luozeng/p/8674529.html)
3. [【linux】分卷压缩-CSDN博客](https://blog.csdn.net/zhicai_liu/article/details/111565472)
4. [linux下分卷压缩/解压缩-CSDN博客](https://blog.csdn.net/u011217649/article/details/71703634)
5. [7z(p7zip)压缩软件在Linux下的安装和使用-腾讯云](https://cloud.tencent.com/developer/article/1389231)
