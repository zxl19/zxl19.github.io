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

### FTP协议

在`文件`->`其他位置`中使用FTP（File Transfer Protocol）协议连接：

```shell
ftp://192.168.1.1
ftps://192.168.1.1
```

### SMB协议

在`文件`->`其他位置`中使用SMB（Server Message Block）协议连接：

```shell
smb://192.168.1.1
```

### SSH协议

1. 在`文件`->`其他位置`中使用SSH（Secure Shell）协议连接：

    ```shell
    sftp://192.168.1.1
    ssh://192.168.1.1
    ```

2. 在命令行中使用SSH协议连接：

    ```shell
    sftp username@192.168.1.1
    ssh username@192.168.1.1
    ```

3. 使用基于SSH协议的`scp`命令远程复制文件：

    ```shell
    scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
        [-l limit] [-o ssh_option] [-P port] [-S program]
        [[user@]host1:]file1 ... [[user@]host2:]file2
    ```

4. OpenSSH是基于SSH协议实现的连接工具，可以使用其提供的`scp`命令获得更快的传输速度；
5. 使用`sshpass`命令非交互式地提供密码：

    ```shell
    sshpass [-f filename|-d num|-p password|-e] [-hV] command arguments
    ```

### Filezilla

在`站点管理器`->`新站点`中添加服务器IP地址：

1. `常规`->`主机`中填写服务器IP地址；
2. `常规`->`协议`中选择传输协议，`FTP`或`SFTP`；
3. `常规`->`登录类型`中选择`正常`；
4. `字符集`中选择`强制UTF-8`保证中文目录名和文件名显示正确；

### obsutil

在命令行中使用`obsutil`命令访问管理华为云对象存储服务（Object Storage Service，OBS）：

```shell
./obsutil [command] [args...] [options...]
```

## 参考

1. [NFS、FTP、SMB、WebDav、DLNA协议，傻傻分不清？-大技术的文章-知乎](https://zhuanlan.zhihu.com/p/411161467)
2. [浅谈FTP，SFTP，FTPS区别-依然范儿特西的文章-知乎](https://zhuanlan.zhihu.com/p/106980723)
3. [Linux scp命令-菜鸟教程](https://www.runoob.com/linux/linux-comm-scp.html)
4. [Why is scp so slow and how to make it faster?-Stack Exchange](https://unix.stackexchange.com/questions/238152/why-is-scp-so-slow-and-how-to-make-it-faster)
5. [sshpass的使用方法-博客园](https://www.cnblogs.com/kaishirenshi/p/7921308.html)
6. [linux之sshpass命令-入门小站的文章-知乎](https://zhuanlan.zhihu.com/p/502078612)
7. [OpenSSH](https://www.openssh.com)
8. [openssh/openssh-portable](https://github.com/openssh/openssh-portable)
9. [obsutil简介-华为云](https://support.huaweicloud.com/utiltg-obs/obs_11_0001.html)
