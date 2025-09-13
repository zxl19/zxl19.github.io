---
layout: post
title: C++数据结构学习笔记
date: 2022-12-28
author: zxl19
tags: [C++, Note]
comments: true
toc: true
pinned: false
---

我的C++数据结构学习笔记。

<!-- more -->

**整理中**

## 链表

### 链表实现

```cpp
struct ListNode {
  int val;                                                 // 当前节点的值
  ListNode* next;                                          // 指向下一个节点的指针
  ListNode() : val(0), next(nullptr) {}                    // 构造函数，初始化当前结点值为0，指针为空
  ListNode(int x) : val(x), next(nullptr) {}               // 构造函数，初始化当前结点值为x，指针为空
  ListNode(int x, ListNode* next) : val(x), next(next) {}  // 构造函数，初始化当前结点值为x，指针非空
};
```

## 二叉树

### 二叉树实现

```cpp
struct TreeNode {
  int val;                                               // 当前节点的值
  TreeNode* left;                                        // 左指针
  TreeNode* right;                                       // 右指针
  TreeNode() : val(0), left(nullptr), right(nullptr) {}  // 构造函数，初始化当前结点值为0，左右指针为空
  TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}  // 构造函数，初始化当前结点值为x，左右指针为空
  TreeNode(int x, TreeNode* left, TreeNode* right)
      : val(x), left(left), right(right) {}  // 构造函数，初始化当前结点值为x，左右指针非空
};
```

### 遍历方式

1. **前序遍历（DLR）**：根在前，从左往右，一棵树的根永远在左子树前面，左子树又永远在右子树前面；
2. **中序遍历（LDR）**：根在中，从左往右，一棵树的左子树永远在根前面，根永远在右子树前面；
3. **后序遍历（LRD）**：根在后，从左往右，一棵树的左子树永远在右子树前面，右子树永远在根前面；

```cpp
// 前序遍历
void pre_order(TreeNode* Node) {
  if (Node == nullptr) return;
  std::cout << "Node Data: " << Node->data << std::endl;
  pre_order(Node->left);
  pre_order(Node->right);
}
// 中序遍历
void middle_order(TreeNode* Node) {
  if (Node == nullptr) return;
  middle_order(Node->left);
  std::cout << "Node Data: " << Node->data << std::endl;
  middle_order(Node->right);
}
// 后序遍历
void post_order(TreeNode* Node) {
  if (Node == nullptr) return;
  post_order(Node->left);
  post_order(Node->right);
  std::cout << "Node Data: " << Node->data << std::endl;
}
```

## 资料

### 教程

1. [数据结构（C++语言版）](https://dsa.cs.tsinghua.edu.cn/~deng/ds/dsacpp/index.htm)
2. [数据结构-C语言中文网](https://c.biancheng.net/data_structure/)
3. [Hello算法](https://www.hello-algo.com)
4. [mikeizbicki/cmc-csci046](https://github.com/mikeizbicki/cmc-csci046)

### GitHub

1. [krahets/hello-algo](https://github.com/krahets/hello-algo)
2. [cp-algorithms/cp-algorithms](https://github.com/cp-algorithms/cp-algorithms)
3. [mandliya/algorithms_and_data_structures](https://github.com/mandliya/algorithms_and_data_structures)
4. [huaxz1986/cplusplus-_Implementation_Of_Introduction_to_Algorithms](https://github.com/huaxz1986/cplusplus-_Implementation_Of_Introduction_to_Algorithms)
5. [ShahjalalShohag/code-library](https://github.com/ShahjalalShohag/code-library)
6. [rachitiitr/DataStructures-Algorithms](https://github.com/rachitiitr/DataStructures-Algorithms)
7. [jainaman224/Algo_Ds_Notes](https://github.com/jainaman224/Algo_Ds_Notes)
8. [0voice/algorithm-structure](https://github.com/0voice/algorithm-structure)
9. [sachuverma/DataStructures-Algorithms](https://github.com/sachuverma/DataStructures-Algorithms)
10. [br7roy/THU-DS](https://github.com/br7roy/THU-DS)
11. [HuyuYasumi/DSA_CPP_Deng](https://github.com/HuyuYasumi/DSA_CPP_Deng)

## 参考

1. [力扣LeetCode](https://leetcode.cn)
2. [链表-腾讯云](https://cloud.tencent.com/developer/article/1656468)
3. [二叉树-CSDN博客](https://blog.csdn.net/u013834525/article/details/80421684)
