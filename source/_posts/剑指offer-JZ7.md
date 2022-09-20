---
title: 剑指offer JZ7
date: 2021-03-01 20:35:47
tags: coding
categories:
- 刷题
- dp
---

# JZ7

[原题链接](https://www.nowcoder.com/practice/c6c7742f5ba7442aada113136ddea0c3)

## 题目

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1）。

## 核心

dp 的基础，斐波那契的路径存储，以利用剪枝

## 思路

经典中的经典，dp 一下路径即可

$T:O(n)$

$S:O(n)$

```c++
class Solution {
public:
    int rectCover(int number) {
        int dp[number + 1];
        memset(dp, 0, sizeof(dp));
        dp[1] = 1;
        dp[2] = 2;
        if (number == 1)return dp[1];
        if (number == 2)return dp[2];
        for (int i = 3; i <= number; i++) dp[i] = dp[i - 1] + dp[i - 2];
        return dp[number];
    }
};
```

