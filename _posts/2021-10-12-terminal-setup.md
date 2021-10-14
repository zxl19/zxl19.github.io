---
layout: post
title: Ubuntu系统终端配置
date: 2021-10-12
author: zxl19
tags: [Ubuntu, Note]
comments: true
toc: true
pinned: false
---

几种Ubuntu系统终端配置方法。

<!-- more -->

## 相关概念区别

1. **terminal（终端）**：文本输入/输出环境；
2. **console（控制台）**：物理终端；
3. **shell**：命令行解释器，包括bash、Zsh等；
4. **bash**：Ubuntu默认的shell；

## bash终端配置

1. 在命令行中右键，选择`配置文件首选项`进行配置：

    - `文本和背景颜色`->勾选`使用系统主题中的颜色`；
    - `文本和背景颜色`->勾选`使用系统主题的透明度`；
    - `调色板`->`内置方案`默认选择`Tango`；
    - `调色板`->勾选`以亮色显示粗体字`；

2. 在`~/.bashrc`文件中使用ANSI转义编码进行配置；

## Zsh+Oh My Zsh终端配置

### Zsh安装及配置

1. 下载并安装Zsh：

    ```shell
    sudo apt install zsh
    ```

2. 查看Zsh是否安装成功：

    ```shell
    zsh --version
    ```

### Oh My Zsh安装及配置

#### 安装

1. 参考[官网](https://ohmyz.sh/)进行安装；
2. 按照提示将系统默认shell设置为Zsh；

#### 配置

1. 在`~/.zshrc`配置文件中配置插件、主题和其他选项；
2. 在[Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki)中可以查看Oh My Zsh自带的和第三方的主题和插件；
3. 每次修改配置文件后都需要重新加载以应用配置：

    ```shell
    source ~/.zshrc
    ```

##### 主题

```text
ZSH_THEME="robbyrussel"     # 默认主题
ZEH_THEME="random"          # 随机主题
ZEH_THEME=""                # 不使用主题
```

###### 自带主题

在[Themes-Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)中查看自带主题。

###### 第三方主题

在[External themes-Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)中查看可供选择的第三方主题以及第三方主题的安装方法。

1. [romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

##### 插件

```text
plugins=(git themes zsh-autosuggestions zsh-syntax-highlighting)
```

###### 自带插件

1. 在[Plugins-Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)中查看自带插件；
2. 在[Plugins Overview-Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins-Overview)中查看按照功能分类的自带插件；

###### 第三方插件

在[External plugins-Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/External-plugins)中查看可供选择的第三方插件以及第三方插件的安装方法。推荐将插件安装在`~/.oh-my-zsh/custom/plugins/`路径下以方便管理。

1. [zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
2. [zsh-users/zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

###### 插件管理

1. [zdharma/zinit](https://github.com/zdharma/zinit)

### 在Zsh终端中使用ROS

1. 若尚未安装ROS，则在安装时配置环境变量：

    ```shell
    echo "source /opt/ros/melodic/setup.zsh" >> ~/.zshrc
    source ~/.zshrc
    ```

2. 若已安装ROS，则仿照`~/.bashrc`文件，在`~/.zshrc`最后添加：

    ```text
    source /opt/ros/melodic/setup.zsh
    ```

3. 在编译功能包后，运行：

    ```text
    source ./devel/setup.zsh
    ```

## 设置终端默认shell

1. 查看当前终端的默认shell：

    ```shell
    echo ${SHELL}
    ```

2. 更改终端默认shell：

    ```shell
    chsh -s /bin/bash       # bash
    chsh -s /usr/bin/zsh    # Zsh
    chsh -s $(which zsh)    # Zsh
    ```

3. 注销或者重启以应用默认shell设置；

## 参考

1. [相关概念区别1-Stack Exchange](https://askubuntu.com/questions/506510/what-is-the-difference-between-terminal-console-shell-and-command-line)
2. [相关概念区别2-博客园](https://www.cnblogs.com/sddai/p/9769086.html)
3. [Update Ubuntu Terminal Color Scheme](https://linuxhint.com/ubuntu_terminal_color_scheme/)
4. [Colours and formatting in Gnome/Ubuntu's Terminal](https://www.growingwiththeweb.com/2015/05/colours-in-gnome-terminal.html)
5. [Oh My Zsh-简书](https://www.jianshu.com/p/b8a80dd59414)
6. [Oh My Zsh-博客园](https://www.cnblogs.com/lcgbk/p/13255836.html)
7. [ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)
8. [配置一个简洁高效的Zsh丨Linux中国-Linux中国的文章-知乎](https://zhuanlan.zhihu.com/p/345559097)
9. [zsh&oh-my-zsh的配置与使用-SCEtoAUX的文章-知乎](https://zhuanlan.zhihu.com/p/58073103)
10. [Ubuntu install of ROS Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu)
11. [安装Zsh后ROS相关命令失效-CSDN博客](https://blog.csdn.net/Amazingren/article/details/81746176)
12. [rosinstall/NonBashShells](http://wiki.ros.org/rosinstall/NonBashShells)
