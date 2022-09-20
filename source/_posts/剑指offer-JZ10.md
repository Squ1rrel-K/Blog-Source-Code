---
title: 剑指offer JZ10
date: 2021-03-01 20:35:56
tags: coding
categories:
- 刷题
- dp
---

# JZ10

[原题链接](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6)

## 题目

我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

## 核心

还是 dp 问题

## 思路

推出状态转移方程

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



