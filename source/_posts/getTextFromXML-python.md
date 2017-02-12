---
title: 使用python处理XML文件
date: 2016-08-03 20:07:49
tags: Python, XML
categories: Programming Language
---

## 前言
本文主要记录我的一段小代码：使用Python从XML文件中提取出想要的信息。主要使用的Element Tree的方法。有涉及到批量处理文件的问题。
<!--more-->

## XML
XML（Extensible Markup Language）是可扩展标记语言，标记（Markup）是关键部分。

## 可以用来解释XML的Python包
> 具体请参考[深入解读Python解析XML的几种方式](http://codingpy.com/article/parsing-xml-using-python/) 

- <font color=red>xml.dom</font>

- <font color=red>xml.dom.minidom</font>

- <font color=red>xml.dom.pulldom</font>

- <font color=red>xml.sax</font>

- <font color=red>xml.parser.expat</font>

- <font color=red>xml.etree.ElementTRee</font>

## 使用Element Tree解析XML

- 像一个轻量级的DOM，将XML看作一棵树，利用对树的操作实现对XML的操作。

- 优点：可用性好，速度快，消耗内存少。

- 两种实现：一种是纯Python实现，例如: xml.etree.ElementTree ，另外一种是速度快一点的:xml.etree.cElementTree。

- 尽量使用C语言实现的那种，因为它速度更快，而且消耗的内存更少! 在2.7程序中可以这样写:
```Python
try:
    import xml.etree.cElementTree as ET
except ImportError:
    import xml.etree.ElementTree as ET
```

- 在Python3中可以直接写ElementTree，会优先调用c语言的实现。

## 使用os.walk()遍历文件夹下的文件

> 具体的细节参考[这篇博客](http://7731023.blog.51cto.com/7721023/1297827)

- 这个函数有三个返回值，可以用于获得路径，文件名等，也可以通过拼接字符串得到具体的路径。

