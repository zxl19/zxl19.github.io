---
layout: post
title: nanoflann库使用笔记
date: 2023-04-11
author: zxl19
tags: [C++, nanoflann, Note]
comments: true
toc: true
pinned: false
---

我的nanoflann库使用笔记。

<!-- more -->

## nanoflann Hello World

1. nanoflann是基于K-D树（K-Dimensional Tree，K-D Tree）的最近邻（Nearest Neighbor，NN）搜索库；
2. nanoflann支持$\mathbb{R}^{2}$、$\mathbb{R}^{3}$欧氏空间，$\mathrm{SO}\left(2\right)$、$\mathrm{SO}\left(3\right)$旋转群上的最近邻搜索；
3. nanoflann使用C++11标准，只由一个头文件构成（header-only），推荐直接将头文件添加到项目中，使用时需要包含头文件：

    ```cpp
    #include "nanoflann.hpp"
    ```

4. 在Ubuntu 21.04及其之后的版本中可以通过软件包管理器安装：

    ```shell
    sudo apt install libnanoflann-dev
    ```

## CMakeLists

```cmake
# 方法一：本地安装（待测试）
find_package(nanoflann REQUIRED QUIET)
# 方法二：非本地安装（推荐）
set(NANOFLANN_INCLUDE_DIRS "${PROJECT_SOURCE_DIR}/third_party/nanoflann")

include_directories(${NANOFLANN_INCLUDE_DIRS})
```

## 最近邻搜索

1. nanoflann支持多种距离指标：

    - $\mathbb{R}^{N}$欧氏空间：
        - `nanoflann::L1`：曼哈顿距离；
        - `nanoflann::L2`：L2范数（默认），支持SSE2指令集，此时输入的搜索半径和返回的最近邻距离都使用L2范数表示；
        - `nanoflann::L2_Simple`：L2范数，用于低维数据，例如点云，此时输入的搜索半径和返回的最近邻距离都使用L2范数表示；
    - $\mathrm{SO}\left(2\right)$旋转群：
        - `nanoflann::metric_SO2`：绝对角度差异；
    - $\mathrm{SO}\left(3\right)$旋转群：
        - `nanoflann::metric_SO3`：四元数之间的内积；

2. K-D树具有一个根节点、若干中间节点以及叶节点：

    - 根节点（root node）指的是只有子节点，没有父节点的节点；
    - 中间节点（intermediary node）指的是既有父节点又有子节点的节点；
    - 叶节点（leaf node）指的是只有父节点，没有子节点的节点；
        - 叶节点中保存着点的索引；
        - 在构建K-D树时，节点被递归分割，直到叶中的叶节点数量小于一定阈值；
        - 叶中的叶节点对应一定范围内的点，在最近邻搜索时，对于叶中的叶节点进行线性搜索；
        - 通过设置叶节点的大小可以实现K-D树的构建速度和最近邻搜索速度之间的权衡（trade-off）：
            - 叶节点大小越大，K-D树的构建速度越快，最近邻搜索速度越慢；
            - 叶节点大小越小，K-D树的构建速度越慢，最近邻搜索速度越快；
            - 在对于最近邻搜索速度要求较高的应用场景中，例如点云匹配，叶节点的大小在10-50较为合适，默认值为10；

3. nanoflann支持多种点云数据结构，在构建K-D树时需要使用对应的适配器（adaptor）；
4. 当多个坐标完全相同的点都是最近邻点时，最近邻搜索返回的最近邻点顺序与其在点云中的保存顺序不具有对应关系；

## 示例

以`std::vector<std::vector<T>>`或`std::vector<Eigen::VectorXd>`的点云数据结构为例，在构建K-D树时需要使用对应的适配器`KDTreeVectorOfVectorsAdaptor`：

```cpp
// C++98/03
typedef std::vector<Eigen::Vector3d, Eigen::aligned_allocator<Eigen::Vector3d>> VVec3d;
typedef KDTreeVectorOfVectorsAdaptor<VVec3d, double> KdtreeType;

// C++11
template <int N, typename T>
using Vec = Eigen::Matrix<T, N, 1>;
template <int N, typename T>
using VVec = std::vector<Vec<N, T>, Eigen::aligned_allocator<Vec<N, T>>>;
using VVec3d = VVec<3, double>;
using KdtreeType = KDTreeVectorOfVectorsAdaptor<VVec3d, double>;

std::size_t dim;
VVec3d samples;
KdtreeType kdtree(dim /*dim*/, samples, 10 /* max leaf */);

// do a knn search
const size_t num_results = 3;
std::vector<size_t> ret_indexes(num_results);
std::vector<double> out_dists_sqr(num_results);

nanoflann::KNNResultSet<double> resultSet(num_results);

resultSet.init(&ret_indexes[0], &out_dists_sqr[0]);
kdtree.index->findNeighbors(resultSet, &query_pt[0], nanoflann::SearchParams());

std::cout << "knnSearch(nn=" << num_results << "): \n";
for (size_t i = 0; i < resultSet.size(); i++) {
  std::cout << "ret_index[" << i << "]=" << ret_indexes[i] << " out_dist_sqr=" << out_dists_sqr[i] << std::endl;
}
```

通过内部实现可以看出，`KDTreeVectorOfVectorsAdaptor`也可以支持自定义点云数据结构，需要满足以下要求：

1. 点云：

    - 具有`size()`成员函数，返回点云中点的总数；
    - 支持通过下标运算符`[]`访问点云中的点；

2. 点：

    - 具有`size()`成员函数，返回点的维度；
    - 支持通过下标运算符`[]`访问点的坐标；

## 参考

1. [jlblancoc/nanoflann](https://github.com/jlblancoc/nanoflann)
