---
title: 剑指offer JZ5
date: 2021-03-01 20:05:21
tags: coding
categories:
- 刷题
- 栈队列
---

# JZ5

## 题目

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

## 核心

栈模拟队列，两个栈捯饬一下即可

## 思路

保持 stack2 在所有操作后为空，只在 pop 时借用

```c++
class Solution {
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        int top=-1;
        //转移至栈2
        while (!stack1.empty()) {
            stack2.push(stack1.top());
            stack1.pop();
        }
        //栈1不空，则栈2必不空
        if (!stack2.empty()) {
            top = stack2.top();
            stack2.pop();
            while (!stack2.empty()) {
                stack1.push(stack2.top());
                stack2.pop();
            }
            return top;
            //栈1空
        } else return NULL;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```

