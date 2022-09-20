---
title: 剑指offer JZ9
date: 2021-03-01 20:35:53
tags: coding
categories:
- 刷题
- dp
---

# JZ9

[原题链接](owcoder.com/practice/22243d016f6b47f2a6928b4313c85387)

## 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

## 核心

dp 题，写出状态转移方程即可

## 思路

$f(n) = \sum\limits_{i=1}^{n-1}f(i)$

$T:O(n)$

$S:O(n)$

```c++
class Solution {
public:
    int jumpFloorII(int number) {
        int dp[number + 1];
        dp[0] = 1;
        for (int i = 1; i <= number; i++) {
            dp[i] = 0;
            for (int j = 0; j < i; j++) {
                dp[i] += dp[j];
            }
        }
        return dp[number];
    }
};
```

