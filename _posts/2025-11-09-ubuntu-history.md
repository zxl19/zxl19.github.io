---
layout: post
title: 在Ubuntu系统中管理命令行历史
date: 2025-11-09
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中管理命令行历史。

<!-- more -->

## 使用`history`命令

### 命令说明

1. `history`命令用于管理命令行历史；
2. 语法说明：

    ```shell
    history [-c] [-d offset] [n]
    history -anrw [filename]
    history -ps arg [arg...]
    ```

### 常用语法

1. 显示带行号的命令历史列表：

    ```shell
    history
    ```

2. 显示最近的`n`条命令（在zsh中会显示从第`n`条开始的所有命令）：

    ```shell
    history n
    ```

3. 以不同格式显示带时间戳的历史记录（仅在zsh中可用）：

    ```shell
    history -d|f|i|E
    ```

4. 清除命令历史列表：

    ```shell
    history -c
    ```

5. 用当前bash的历史记录覆盖历史文件（通常与`history -c`结合使用以彻底清除历史）：

    ```shell
    history -w
    ```

6. 删除指定偏移量`offset`处的历史记录条目：

    ```shell
    history -d offset
    ```

7. 将一条命令添加到历史记录中，但不运行：

    ```shell
    history -s command
    ```

8. 通过在命令前添加一个空格，来运行命令且不将其添加到历史记录中：

    ```shell
    <space>command
    ```

## 扩展用法

1. 以root权限运行上一条命令（`!!`会被替换为上一条命令）：

    ```shell
    sudo !!
    ```

2. 使用上一条命令的最后一个参数来运行一条新命令：

    ```shell
    command !$
    ```

3. 使用上一条命令的第一个参数来运行一条新命令：

    ```shell
    command !^
    ```

4. 运行历史记录中的第`n`条命令：

    ```shell
    !n
    ```

5. 运行历史记录中的倒数第`n`条命令：

    ```shell
    !-n
    ```

6. 运行最近一条包含字符串`string`的命令：

    ```shell
    !?string?
    ```

7. 重新运行上一条命令，但将其中的字符串`string1`替换为字符串`string2`：

    ```shell
    ^string1^string2^
    ```

8. 执行一次历史扩展，但只打印将要运行的命令，并不运行：

    ```shell
    !-n:p
    ```
