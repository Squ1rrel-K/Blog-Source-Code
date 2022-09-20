---
title: EditorConfig 使用说明
date: 2022-09-20 15:25:29
tags: coding
---

# EditorConfig 使用说明

.EditorConfig 文件是为了保证跨 IDE 的代码一致性，以避免不同缩进方式带来的潜在安全问题

.EditorConfig 的优先级高于 IDE



## 查询表

```
# 表示是最顶层的配置文件，发现值为true时，才会停止查找.editorconfig文件
root
 
# 设置使用那种缩进风格(tab是制表符，space是空格)
indent_style
 
# 定义用于每个缩进级别的空格数
indent_size
 
# 用一个整数来设置tab缩进的列数。
tab_width
 
# 设置换行符，值为lf、cr和crlf
end_of_line
 
# 设置编码格式，值为latin1、utf-8、utf-8-bom、utf-16be和utf-16le
charset
 
# 设置为true则删除换行符之前的任何空白字符
# 设置为true会删除每一行后的任何空格  ***
trim_trailing_whitespace
 
# 设置为true以确保文件在保存时以换行符结尾
# 如果设置为true，则文件最后一行也会确保以换行符结尾，会强制换行到下一行  ***
insert_final_newline
```

## 通配方式

##### *

任何字符串，路径分隔符 (  / ) 除外

##### **	

任何字符串

##### ?	

任何单个字符，路径分隔符  ( / ) 除外

##### [name]	

匹配名称中的任何单个字符

##### [!name]	

匹配名称中没有的任何单个字符

##### {s1,s2,s3}	

匹配任何给定的字符串（以逗号分隔，可以嵌套）

##### {num1..num2}	

num1 和之间的任何整数 num2，其中 num1 和 num2 可以是正数或负数



匹配到的不同的文件类型，可以定义不同的格式化属性。

特殊字符可以用反斜杠转义，这样它们就不会被解释为通配符模式。