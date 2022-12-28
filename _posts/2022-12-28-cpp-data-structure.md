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
    int val;                                    // 当前节点的值
    struct ListNode *next;                      // 指向下一个节点的指针
    ListNode(int x) : val(x), next(nullptr) {}  // 初始化当前结点值为x，指针为空
};
```

## 二叉树

### 二叉树实现

```cpp
struct TreeNode {
    int val;                                                    // 当前节点的值
    TreeNode *left;                                             // 左指针
    TreeNode *right;                                            // 右指针
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}  // 初始化当前结点值为x，左右指针为空
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

## 参考

1. 《C++语言程序设计》
2. [数据结构-C语言中文网](http://c.biancheng.net/data_structure/)
3. [链表-腾讯云](https://cloud.tencent.com/developer/article/1656468)
4. [二叉树-CSDN博客](https://blog.csdn.net/u013834525/article/details/80421684)
