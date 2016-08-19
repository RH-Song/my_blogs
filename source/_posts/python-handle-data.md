---
title: python对数据的预处理
date: 2016-05-10 09:38:13
tags: Python
categories: DataMining
---
# 数据的读入
- with关键字 
使用with关键字，可以在open file之后，with结束时文件自动关闭，不需要再使用close。是一个不错的选择。
<!--more-->
- numpy数组
可以读入到numpy的数组中。如果对于读入的数据的形态不够满意，可以使用reshape进行修改。
``` Python
a = numpy.loadtxt('filename.txt')
```
``` Python 
b = numpy.reshape(a,(希望的形态))
b = numpy.reshape(a,(-1,1,2))
```

- 存入list
只是读出来，并存入一个list。
``` Python
with open('training.txt','r') as f:
	data = f.readlines()
	for line in data:
		odom = line.split()
# change data into float
		numbers_float = map(float, odom)
		print numbers_float
```
