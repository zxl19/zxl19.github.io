---
layout: post
title: COLMAP使用笔记
date: 2021-12-10
author: zxl19
tags: [SLAM, Note]
comments: true
toc: true
pinned: false
---

三维重建工具COLMAP使用笔记。

<!-- more -->

## 安装

```shell
sudo apt install colmap
```

## 运行

### 在命令行中

```shell
colmap -h
```

### 在可视化界面中

```shell
colmap gui
```

## 重建步骤

### 新建项目

1. `File`->`New Project`；
2. 设置`Database`为存储`.db`文件的路径；
3. 设置`Images`为存储图片的路径；

### 特征提取

1. `Processing`->`Feature extraction`；
2. `Camera model`根据相机结构选择，以`PINHOLE`为例；
3. 勾选`Custom Parameters`，输入预先标定的相机内参（中间无空格分隔），`PINHOLE`相机模型内参包括`fx,fy,cx,cy`；
4. 如有GPU，勾选`use_gpu`；
5. 点击`Extract`；

### 特征匹配

1. `Processing`->`Feature matching`；
2. 选择匹配方法，以`Exhaustive`为例，经测试相比于`Sequential`耗时更长，但重建效果更好；
3. 如有GPU，勾选`use_gpu`；
4. 点击`Run`；

### 三维重建

1. `Reconstruction`->`Reconstruction Options`->`Bundle`->`Camera parameters`，取消勾选`refine_focal_length`、`refine_principal_point`、`refine_extra_params`；
2. `Reconstruction`->`Start reconstruction`；

### 结果保存和查看

#### 结果保存

1. `File`->`Save project`，替换保存`project.ini`文件；
2. `File`->`Export model as text`，导出重建结果；

#### 结果查看

1. `File`->`Import model`导入重建结果；

## 注意事项

1. 建议在重建前先标定相机内参，在重建过程中设置不优化相机内参，防止重建失败；
2. 使用ZED 2相机可以获得去畸变后的图片以及对应的相机内参（发布在camera_info话题中，每次开机自标定后内参会有细微不同），此时可直接采用`PINHOLE`相机模型；
3. 一般来说采用`OpenCV`相机模型可以满足要求，模型参数包括`fx,fy,cx,cy,k1,k2,p1,p2`，在标定时径向畸变和切向畸变选择两参数模型；
4. [Xbbei/super-colmap](https://github.com/Xbbei/super-colmap)使用[SuperPoint](https://github.com/magicleap/SuperPointPretrainedNetwork)代替COLMAP原来使用的SIFT特征来提取特征点，获得了更加鲁棒的特征点，提高了重建结果的质量，[zxl19/super-colmap](https://github.com/zxl19/super-colmap)在其基础上添加了手动回环检测；
5. 迭代结束时重投影误差一般在0.8个像素左右；

## 参考

1. [colmap/colmap](https://github.com/colmap/colmap)
2. [COLMAP Documentation](https://colmap.github.io/)
3. [Xbbei/super-colmap](https://github.com/Xbbei/super-colmap)
4. [magicleap/SuperPointPretrainedNetwork](https://github.com/magicleap/SuperPointPretrainedNetwork)
5. [rpautrat/SuperPoint](https://github.com/rpautrat/SuperPoint)
