---
layout: post
title: 在Ubuntu系统中使用服务器
date: 2022-07-12
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统中使用服务器，服务器IP地址以`192.168.1.1`为例。

<!-- more -->

## 连接方式

### FTP

在`文件`->`其他位置`中使用FTP（File Transfer Protocol）协议连接：

```shell
ftp://192.168.1.1
```

### SMB

在`文件`->`其他位置`中使用SMB（Server Message Block）协议连接：

```shell
smb://192.168.1.1
```

### SSH

在命令行中使用SSH连接：

```shell
ssh username@192.168.1.1
```

使用基于SSH的scp命令远程复制文件：

```shell
scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
    [-l limit] [-o ssh_option] [-P port] [-S program]
    [[user@]host1:]file1 ... [[user@]host2:]file2
```

### Filezilla

在`站点管理器`->`新站点`中添加服务器IP地址：

1. `常规`->`主机`中填写服务器IP地址；
2. `常规`->`协议`中选择传输协议，`FTP`或`SFTP`；
3. `常规`->`登录类型`中选择`正常`；
4. `字符集`中选择`强制UTF-8`保证中文目录名和文件名显示正确；

## 参考

1. [Linux scp命令-菜鸟教程](https://www.runoob.com/linux/linux-comm-scp.html)