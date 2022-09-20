---
title: 剑指offer JZ6
date: 2021-03-01 20:24:01
tags: coding
categories:
- 刷题
- 数组
---

# JZ6

[原题链接](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba)

## 题目	

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

## 核心

看似简单，实则考虑数组查找的优化问题

## 思路

### 傻乎乎遍历 2分

$T:O(\frac{n}{2} )$

$S:O(1)$

要不就不转，第一个元素是最小，要不就转，那突然下落的地方肯定是最小元素

```c++
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        if (rotateArray.empty()) return 0;
        int min = rotateArray[0];
        for (int i = 0; i < rotateArray.size() - 1; i++) {
            if (rotateArray[i] > rotateArray[i + 1]) {
                min = rotateArray[i + 1];
                break;
            }
        }
        return min;
    }
};
```

### 二分法 5分