---
title: 体验新的主题：NexT
date: 2016-07-16 02:12:22
tags: NexT
categories: Hexo
---
## 摘要
文章主要谈一下新使用的一个Hexo主题Next的使用体验，顺带唠叨一些不那么重要的东西。
<!--more-->
## Why
首先谈一下为什么需要找个新的主题，主要是希望可以改善一下blog的界面，同时可以有更多的功能实现。然而本人又比较懒，不想自己捣鼓代码，所以就寻找新的主题，希望找到在界面上更加简洁明了，功能上整合了访问统计，阅读统计，评论系统等。

## How
怎么找到这个Hexo的主题NexT的呢？通过知乎了解一些主题之后，去到Github上去搜索，最终锁定目标为next。

## 配置
首先，附上[配置教程](http://theme-next.iissnan.com/getting-started.html#install-next-theme)。
配置过程最大的好感是配置文档写得详细清晰，使得配置过程还算是比较顺当的，除了对于每篇文章的统计数据以外。其实就是个人觉得做这个每篇统计过程稍微繁琐了一些，而且是每篇blog写好之后，还要手动的去进行后台的管理设置，如果我的理解没有错误的话。百度统计，多说评论都已经成功了，暂缺对于每一篇的阅读数量统计，留待以后再完成吧。

## 解决tags和categories页面错误的问题
- 进入source/categories,将index.md删除，进入source/tags，将index.md删除。
- 在博客根目录下运行
```
$ hexo new page "tags"
$ hexo new page categories
```
- 在source/tags/index.md中添加: type: "tags"
- 在source/categories/index.md中添加: type: "categories"
- 修改后如图：
![index.png](theme-next/index.png)
