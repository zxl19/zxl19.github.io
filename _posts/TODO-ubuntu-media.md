---
layout: post
title: 在Ubuntu系统中处理音视频文件
date: TODO
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中处理音视频文件。

<!-- more -->

## 使用`ffmpeg`命令

### 命令说明

1. `ffmpeg`命令用于进行视频转换；
2. 语法说明：

    ```shell
    ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...
    ```

### 常用语法

```shell
ffmpeg -i input_video.mp4 -vf setpts=PTS/2 -af atempo=2 output_video.mp4
```

## 使用`ffprobe`命令

### 命令说明

1. `ffprobe`命令用于获取音视频文件的信息；
2. 语法说明：

    ```shell
    ffprobe [options] [input_url]
    ```

### 常用语法

## 使用`ffplay`命令

### 命令说明

1. `ffplay`命令用于播放音视频文件；
2. 语法说明：

    ```shell
    ffplay [options] [input_url]
    ```

### 常用语法

## 参考

1. [FFmpeg](https://ffmpeg.org)
2. [FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg)
3. [ffmpeg音视频倍速播放-于道的文章-知乎](https://zhuanlan.zhihu.com/p/677539222)
4. [用ffmpeg加速播放视频的方法-百度经验](https://jingyan.baidu.com/article/cd4c29795564c1756e6e6099.html)
