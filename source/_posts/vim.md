---
title: vim
date: 2016-07-15 11:25:30
tags: vim
categories:
---
## 前言
本文意在记录vim的使用以及相关的配置。
<!--more-->

## 在linux下vim中文出现乱码问题

> 引用自[这篇博客](http://www.cnblogs.com/joeyupdo/archive/2013/03/03/2941737.html)

- 解决办法，在.vimrc文件中添加以下代码即可以解决：
```shell
set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
set termencoding=utf-8
set encoding=utf-8
```

- Vim的四个字符编码方式
  + encoding
  + fileencoding
  + fileencodings
  + termencoding

- 借用别人的一段话：“由于 Unicode 能够包含几乎所有的语言的字符，而且 Unicode 的 UTF-8 编码方式又是非常具有性价比的编码方式 (空间消耗比 UCS-2 小)，因此建议 encoding 的值设置为 utf-8。这么做的另一个理由是 encoding 设置为 utf-8 时，Vim 自动探测文件的编码方式会更准确 (或许这个理由才是主要的 ;) 。我们在中文 Windows 里编辑的文件，为了兼顾与其他软件的兼容性，文件编码还是设置为 GB2312/GBK 比较合适，因此 fileencoding 建议设置为 chinese (chinese 是个别名，在 Unix 里表示 gb2312，在 Windows 里表示 cp936，也就是 GBK 的代码页)。”

## vim：MarkDown preview
- 借助Chrome的插件markdown preview plus，记住记住记住！！！进入Chrome的管理扩展程序，勾选上Markdown Preview Plus的允许访问文件网址。不然的话是没有办法正常使用这个扩展程序的。

- 勾选上允许访问文件网址之后，在网址输入框输入文件路径即可看到预览。

- 这个扩展程序允许选择自动刷新时间，主题，css等。

## MarkDown:md文件转为pdf文件
- 使用Chrome的预览插件打开预览，然后使用打印功能，即可保存为PDF文件。效果还是很棒的。

## vim添加markdown语法高亮
> 使用[plasticboy/vim-markdown](https://github.com/plasticboy/vim-markdown)

- 步骤如下（使用Vundle管理vim插件，其它的管理方式的安装方法可以参考原链接的内容）：
  + 在.vimrc中添加：
  ```
  Plugin 'godlygeek/tabular'
  Plugin 'plasticboy/vim-markdown'
  ```
  + 在vim运行：
  ```
  :so ~/.vimrc
  :PluginInstall
  ```
