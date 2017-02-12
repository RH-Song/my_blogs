---
title: Ubuntu 安装远程桌面 
date: 2016-06-07 10:46:06
tags: remote-controll, desktop
categories: Linux
---
本文主要解决通过Windows自带的远程桌面，连接到Ubuntu。
<!--more-->
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
