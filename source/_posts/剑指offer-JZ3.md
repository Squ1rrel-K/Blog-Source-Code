---
title: 剑指offer JZ3
date: 2021-03-01 16:37:35
tags: coding
categories:
- 刷题
- 链表
---

# JZ3

[原题链接](nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035)

## 题目

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

## 核心

链表翻转，可提出可直接模拟

## 思路

### 提出法（包括栈模拟，数组翻转，反向迭代器）

数据提出来扔 vector 里，在输出即可，不是真正的翻转链表，仅数据反向输出

$T:O(n)$

$S:O(n)$

```c++
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode *head) {
        vector<int> list;
        while (head != nullptr) {
            list.push_back(head->val);
            head = head->next;
        }
        reverse(list.begin(), list.end());
        return list;
    }
};
```

### 模拟法

真实模拟链的变换，若题目需要输出 list 而非 vector 则此方法为好方法

