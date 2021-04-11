---
layout: post
title: 在Ubuntu系统下安装MATLAB
date: 2020-08-29
author: zxl19
tags: [MATLAB, Ubuntu]
comments: true
toc: true
pinned: false
---

记录一下如何在Ubuntu系统下安装MATLAB R2020a。

<!-- more -->

## 操作步骤

1. 挂载`.iso`镜像；

    ```shell
    #在media目录下创建matlab文件夹供挂载
    sudo mkdir /media/matlab
    #挂载R2020a.iso镜像文件，注意镜像文件所在路径
    sudo mount -t auto -o loop ~/R2020a.iso /media/matlab/
    ```

2. 运行安装文件；

    ```shell
    sudo /media/matlab/install
    ```

    之后的安装选项与Windows中相同，注意勾选`创建指向以下位置中的MATLAB脚本的符号链接`。

3. 卸载镜像

    ```shell
    sudo umount /media/matlab
    ```

4. 设置快捷方式。

    ```shell
    sudo gedit /usr/share/applications/Matlab2020a.desktop
    ```

    添加以下内容，具体按照自己的安装路径修改：

    ```text
    [Desktop Entry]
    Encoding=UTF-8
    Name=Matlab R2020a
    Comment=MATLAB
    Exec=/usr/local/MATLAB/R2020a/bin/matlab
    Icon=/usr/local/MATLAB/R2020a/toolbox/shared/dastudio/resources/MatlabIcon.png
    Terminal=true
    StartupNotify=true
    Type=Application
    Categories=Application;
    ```

## 添加工具箱

1. 进入工具箱目录，修改权限；

    ```shell
    cd /usr/local/MATLAB/R2020a
    sudo chmod 777 toolbox
    ```

2. 添加工具箱；
3. 在MATLAB中设置路径：

    `设置路径`->`添加并包含子文件夹`->`保存`

    出现提示后再次修改权限：

    ```shell
    sudo chmod 777 -R toolbox
    ```

## 注意事项

**不要安装matlab-support！！！**

## 设置快捷键

Ubuntu系统中的快捷键默认采用Emacs默认集，可以采用如下方式进行修改：

`预设`->`MATLAB`->`键盘`->`快捷方式`->`Windows默认集`

## 参考

1. [安装-博客园](https://www.cnblogs.com/taoyuyeit/p/8823311.html)
2. [添加工具包-CSDN博客](https://blog.csdn.net/will_ye/article/details/79645447)
3. [快捷键设置-CSDN博客](https://blog.csdn.net/brandyzhaowei/article/details/7895298)
