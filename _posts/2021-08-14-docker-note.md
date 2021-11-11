---
layout: post
title: Docker学习笔记
date: 2021-08-14
author: zxl19
tags: [Docker, Note]
comments: true
toc: true
pinned: false
---

我的Docker学习笔记。

<!-- more -->

## Docker Hello World

### Docker架构

三个基本概念：

1. **镜像（Image）**：类似于面向对象中的类；
2. **容器（Container）**：类似于面向对象中的对象；
3. **仓库（Repository）**：用于保存镜像；

## Docker常用命令

### 容器生命周期管理

| 功能 | 命令 |
| :------ | :------ |
| 创建一个新的容器并运行一个命令 | `docker run` |
| 启动/停止/重启容器 | `docker start/stop/restart` |
| 杀掉一个运行中的容器 | `docker kill` |
| 删除一个或多个容器 | `docker rm` |

### 容器操作

| 功能 | 命令 |
| :------ | :------ |
| 列出容器 | `docker ps` |

### 镜像仓库

| 功能 | 命令 |
| :------ | :------ |
| 登入/登出一个Docker镜像仓库 | `docker login/logout` |
| 从镜像仓库中拉取或者更新指定镜像 | `docker pull` |
| 将本地的镜像上传到镜像仓库 | `docker push` |

### 本地镜像管理

| 功能 | 命令 |
| :------ | :------ |
| 列出本地镜像 | `docker images` |
| 删除本地一个或多个镜像 | `docker rmi` |

## 解决运行Docker需要sudo问题

### 产生原因

Docker进程使用Unix socket而不是TCP端口。而默认情况下，Unix socket属于root用户，需要root权限才能访问。

### 解决方法

1. 查看用户组：

    ```shell
    cat /etc/group | grep docker
    ```

2. 如果未创建，在此步创建用户组，若已创建，执行下一步：

    ```shell
    sudo groupadd docker
    ```

3. 将用户加入到用户组：

    ```shell
    sudo usermod -aG docker <用户名>
    ```

4. 检查是否成功加入：

    ```shell
    cat /etc/group
    ```

5. 重启Docker：

    ```shell
    sudo systemctl restart docker
    ```

6. 给`docker.sock`文件添加权限：

    ```shell
    sudo chmod a+rw /var/run/docker.sock
    ```

7. 确认是否解决：

    ```shell
    docker run hello-world
    ```

## 参考

1. [Docker教程-菜鸟教程](https://www.runoob.com/docker/docker-tutorial.html)
2. [Docker Hub](https://hub.docker.com/)
3. [Docker启动Get Permission Denied-博客园](https://www.cnblogs.com/informatics/p/8276172.html)
4. [解决运行docker命令要用sudo的问题-博客园](https://www.cnblogs.com/zyh1994/p/13688542.html)
5. [解决运行docker命令要用sudo的问题-简书](https://www.jianshu.com/p/1354e0506753)
