---
title: python入门笔记
date: 2016-05-14 10:08:50
tags: Python
categories: programming language
---
# 前言
这是一篇学习Python的入门笔记。
<!--more-->

# 语句
- 注释：#
- 代码块：缩进
- 反斜线：\ 继续上一行

# 变量赋值
- 乘方：**
- 两个数的交换：
``` Python
x = 1
y = 2
x,y = y,x
```

# 风格
- 下划线：
_xxx 不用from inport *导入
__XXX__ 系统定义名字
__XXX 类中的私有变元

- PEP07 PEP08 PEP20 PEP257

- 模块和布局
startup line
Module documentation
Module Import
(Global) Variable declaration
class declaration
Function declaration
main body

- 动态类型
- 内存分配
- del语句：变量引用减少
- 局部变量替换模块变量

# 变量
- 列表 使用[]
- 元组 使用()
- 字典 {}

# 切片
多维切片：sequence[start1:end1,start2:end2,...]
步进切片：sequence[start1:end1:stepLength]

判断类型：isinstance

# 序列下标
顺序为: 0,1,2,3....,(N-1)
逆序为:-N,-(N-1),....,1

# 序列类型操作符
- 成员类型操作符
in \ not in
seq[ind]
seq[ind1:ind2]
seq * expr 序列重复expr次
seq1 + seq2
obj in seq
obj not in seq
seq[::2]

- BIF
list()
str()
unicode()
basestring()
tuple()
enumerate(iter) 生成由iter每个元素的index值和item值组成的tuple
len(seq)
max(iter,key=None)
min(iter, key=None)
reversed(seq)
sorted(iter, func=Nome, key=Nome, reverse=False)
sum(seq, init=0)
zip([it0,it1,....itN]) 返回列表,其中第一个元素变成一个元组,第二个...类推

- 字符串
改变一个字符串必须通过创建一个新的字符串产生,不能单独改变字符串的某一个字符或者子串.但是可以被一个旧串的某个部分或者一个新串拼凑或者替换

- 格式化操作符辅助指令
* 定义宽度或者小数点精度
- 左对齐
+ 正数面前加上+
<sp> 在正数前面显示空格
# 8进制16进制前面有0
0 在显示的数字前面显示0而不是默认的空格
% 辅助输出%
(var) 映射变量
m.n m表示最小总宽度,n是小数点后的位数
r/R 原始字符

# 列表
- 生成:a = []  list('foo')
- 访问:a[1] a[1:4](支持切片操作)
- 更新:a[2] = '...' 使用append()进行追加
- 删除:del a[1] a.remove(123)
- 连接操作符:+ extend() +=
- 内置函数

# 元组
- 与列表非常像
- 使用list()和tuple()进行相互转换

