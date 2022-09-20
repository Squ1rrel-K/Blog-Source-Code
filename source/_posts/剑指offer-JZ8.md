---
title: 剑指offer JZ8
date: 2021-03-01 20:35:50
tags: coding
categories:
- 刷题
- dp
---

# JZ8

[原题链接](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4)

## 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

## 核心

dp 题，写出状态转移方程即可

## 思路

$f[n] = f[n-2] + f[n-1]$

$T:O(n)$

$S:O(n)$

```c++
class Solution {
public:
    int jumpFloor(int number) {
        int dp[number + 1];
        dp[0] = 1;
        dp[1] = 1;
        if (number == 1) return dp[1];
        for (int i = 2; i <= number; i++) {
            dp[i] = dp[i - 2] + dp[i - 1];
        }
        return dp[number];
    }

};
```

