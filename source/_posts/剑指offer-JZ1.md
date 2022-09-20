---
title: 剑指offer JZ1
date: 2021-03-01 13:30:31
tags: coding
categories:
- 刷题
- 数组
---

# JZ1

[原题链接](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e)

## 题目

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## 核心

数组遍历与优化，元素有序易想到二分法，观察法不易想到

## 思路 M行N列

### 暴力枚举 1分

一个个查，不好，浪费了两个方向有序的条件

$T: O(mn)$

$S: O(1)$

```c++
class Solution {
public:
    bool Find(int target, vector <vector<int>> array) {
        //空数组
        if (array.size() == 0 || array[0].size() == 0) return false;
        //遍历
        for (int i = 0; i < array.size(); i++) {
            for (int j = 0; j < array[0].size(); j++) {
                if (target == array[i][j]) return true;
            }
        }
        return false;
    }
};
```

### 行二分 2分

一行行查，每行的数使用二分法

$T: O(mlogn)$

$S:O(1)$

```c++
class Solution {
public:
    bool Find(int target, vector <vector<int>> array) {
        //空数组
        if (array.size() == 0 || array[0].size() == 0) return false;
        //行遍历
        for (int i = 0; i < array.size(); i++) {
            int left = 0, right = array[0].size() - 1;
            //每行的数二分
            while (left <= right) {
                int mid = (left + right) / 2;
                if (target == array[i][mid]) return true;
                else if (target > array[i][mid]) {
                    left = mid + 1;
                } else if (target < array[i][mid]) {
                    right = mid - 1;
                }
            }
        }
        return false;
    }
};
```

### 观察法（副对角线顶点法）5分

妙啊！

右上角（左下角）的节点一定是该行最大，该列最小的，比较后按照大小关系移动即可

$T:O(n)$, $n=max(M,N)$

$S:O(1)$

```c++
class Solution {
public:
    bool Find(int target, vector <vector<int>> array) {
        //空数组
        if (array.size() == 0 || array[0].size() == 0) return 0;
        int x = 0, y = array[0].size() - 1, val;
        //元素在数组范围内移动
        while (x >= 0 && x < array.size() && y >= 0 && y < array[0].size()) {
            val = array[x][y];
            if (target == val) return true;
            //大于，下移
            else if (target > val) x++;
            //小于，左移
            else if (target < val) y--;
        }
        return false;
    }
};
```

