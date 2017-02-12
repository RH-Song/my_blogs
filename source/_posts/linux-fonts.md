---
title: 为Linux系统增加字体
date: 2016-06-03 22:09:43
tags: fonts 
categories: Linux
---
## 增加字体
<!--more-->

作为一个打算将Linux作为常用系统的用户，就要学会自己解决一些问题。字体安装就是很小的一个事情，但是不可避免的。因为在写论文，写报告的时候，需要使用到一些windows下常用的字体，但是linux下并没有自带，所以我们需要自己安装。
字体是ttf文件，可以互联网上的字体下载网站上下载，可以从github上下载，也可以从Windows上copy过来。
安装方法：
- 把文字的ttf文件cp到/usr/share/fonts/下，也可以在该文件夹下新建一个文件夹再放进去
- 再该文件夹下执行：
``` bash
$ sudo mkfontscale
$ sudo fc-cache
```
这样就安装完成了。


## vim插件使用
- cscope：vim下查看文件，实现文件跳转
- ctags：代码标签跳转



## 命令行安装deb包
```shell
sudo dpkg -i filename
```
