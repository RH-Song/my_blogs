---
title: linux使用记录
date: 2016-06-03 22:09:43
tags: 
categories: Linux
---
前言：这些修改主要实现在Ubuntu14.04上的。不过其他版本很多时候也可以支持。

<!--more-->

## 增加字体
作为一个打算将Linux作为常用系统的用户，就要学会自己解决一些问题。字体安装就是很小的一个事情，但是不可避免的。因为在写论文，写报告的时候，需要使用到一些windows下常用的字体，但是linux下并没有自带，所以我们需要自己安装。
字体是ttf文件，可以互联网上下载，来源很多，但是推荐从github上下载，个人认为更干净。
安装方法：
- 把文字的ttf文件cp到/usr/share/fonts/下，也可以在该文件夹下新建一个文件夹再放进去
- 再该文件夹下执行：
``` bash
$ sudo mkfontscale
$ sudo fc-cache
```
这样就安装完成了。

## 通过windows远程桌面Ubuntu 14.04
- 安装xrdp：
```shell
sudo apt-get install xrdp
```
- 安装vnc4server：
```shell
sudo apt-get install vnc4server
```
- 安装xUbuntu：
```shell
sudo apt-get install xubuntu-desktop
```
- 使用xfce4：echo "xfce4-session" >~/.xsession
- 重启xrdp：
```shell
sudo service xrdp restart
```
这样便可以使用windows远程桌面连接，连接到Ubuntu。
后记：这样做以后是有风险的，因为安装了xUbuntu桌面，所以重启之后桌面会变为xUbuntu的风格，如有需要，可以重新设置。当然网络上还有其他的教程不需要重新安装一个桌面系统的。
## Docky的使用
对于一个希望拥有灵活的任务栏的人，或者你希望拥有mac风格的任务栏，推荐使用Docky。
貌似Docky好几种，我使用的是在Ubuntu应用商店中直接搜索Docky，出现的那一个，效果是不错的，
可以查找一个你喜欢的Docky主题，我使用的是Buyi-iDocky

## vim插件使用
- cscope：vim下查看文件，实现文件跳转
- ctags：代码标签跳转

## 移动硬盘的使用
很多时候移动硬盘在Ubuntu下是没有出现一个类似于windows一样的图标，点击即可进入，那应当如何在命令行中查看呢？或者找到相应的位置然后访问呢？或者让移动硬盘的内容出现在合适的我们希望的地方，我们可以进行访问呢？
### 步骤如下：
- sudo fdisk -l:可以查看到系统中所有的已经存在的磁盘，根据大小和相关信息可以推测出哪一个是我们的移动硬盘
![查看设备](linux_fonts/mymv.png)
- mount:查看挂载的设备。当然可以看到我们的移动硬盘是是否已经挂载。如果已经挂载是被挂载到哪个路径下，可以根据此路径进行访问。
![查看挂载情况](linux_fonts/mvpath.png)
此外，还可以自己再进行挂载或者断开挂载：
假设移动硬盘是：/dev/sdc 期待的挂载点：/mnt/mvdisk
```shell
$ sudo mount /dev/sdc /mnt/mvdisk (挂载)
$ sudo umount /mnt/mvdisk (断开挂载)
```

## Ubuntu右上角的错误
错误提示为：Update information is outdated...
- step1：运行```$sudo apt get update```
- step2：根据最后输出的信息错误进行修改，具体的修改方案参考这篇[博客](https://linux.cn/article-5603-1.html#3_447)
简单记录几种情况：
1. problems with merge lists
```shell
$sudo rm -r /var/lib/apt/lists/*
$sudo apt-get clean && sudo apt-get update
```
2. Failed to fecth ... Package Hash Sum mismatch
```shell
$sudo rm -rf /var/lib/apt/lists/*
$sudo apt-get update
```
3. ppa过时导致的
找到software&update->other software->去掉过时的那个ppa前面的勾或者直接删除
4. 从某个网址下载失败
找到Software&Update->Ubuntu Software,更换源
5. not all update can install
```shell
$sudo apt-get install -f
```
6. error while loading shared libraries:
```shell
$sudo /sbin/ldconfig -v
```
7. Could not get lock /var/cache/apt/archives/lock
这个是因为你在其他地方在安装某个东西，而又在这里使用到apt
```shell
$sudo rm /var/lib/apt/lists/lock
```
或者
```shell
$sudo killall apt-get
```
8. 下列签名无法验证
假设不能添加的key为： 68980A0EA10B4DE8
```shell
$sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 68980A0EA10B4DE8
```
9. 如何是像这样的签名错误：The following signatures were invalid: BADSIG 16126D3A3E5C1192 Ubuntu Extras Archive Automatic Signing Key
```shell
sudo apt-get clean
cd /var/lib/apt
sudo mv lists oldlist
sudo mkdir -p lists/partial
sudo apt-get clean
sudo apt-get update
```

## 命令行安装deb包
```shell
sudo dpkg -i filename
```
