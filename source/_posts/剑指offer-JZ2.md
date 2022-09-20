---
title: 剑指offer JZ2
date: 2021-03-01 15:36:32
tags: coding
categories:
- 刷题
- 字符串
---

# JZ2

[原题链接](https://www.nowcoder.com/practice/0e26e5551f2b489b9f58bc83aa4b6c68)

## 题目

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

## 核心

字符串替换，STL 简单处理

## 思路

### stl string.replace()

$T:O(n)$

$S:O(1)$

```c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param s string字符串 
     * @return string字符串
     */
    string replaceSpace(string s) {
       for(int i=0;i<s.size();i++){
           if(s[i]==' ') s.replace(i,1,"%20");
       }
        return s;
    }
};
```

