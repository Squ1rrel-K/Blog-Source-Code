---
title: 剑指offer JZ4
date: 2021-03-01 17:51:37
tags: coding
categories:
- 刷题
- 树
---

# JZ4

[原题链接](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6)

## 题目

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

## 核心

中序+其他序造树，分随机存储（数组），顺序存储（链表）两种，找 root 两边 dfs 递归即可，PAT 送分题

## 思路

### 常规题

$T:O(n)$

$S:O(n)$

```c++
class Solution {
public:
    TreeNode *reConstructBinaryTree(vector<int> pre, vector<int> vin) {
        return buildTree(pre, vin, 0, pre.size() - 1, 0, vin.size() - 1);
    }

    TreeNode *buildTree(vector<int> &pre, vector<int> &vin, int preL, int preR, int inL, int inR) {
        //返回
        if (preL > preR) return NULL;
        //新根
        TreeNode *root = new TreeNode(pre[preL]);
        //找 vin 中的根
        int i;
        for (i = inL; i <= inR; i++) {
            if (pre[preL] == vin[i]) break;
        }
        //递归子树
        int numLeft = i - inL;
        root->left = buildTree(pre, vin, preL + 1, preL + numLeft, inL, i - 1);
        root->right = buildTree(pre, vin, preL + numLeft + 1, preR, i + 1, inR);
        return root;
    }
};
```

