---
title: 解决Ubuntu update时候遇到的错误 
date: 2016-02-07 10:55:40
tags: issue
categories: Linux
---

本文记录如何解决Ubuntu update时候遇到的错误。
<!--more-->
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
