---
title: Ubuntu下磁盘挂载和查看 
date: 2016-02-07 11:01:34
tags: mount，disk
categories: Linux
---
## Ubuntu下磁盘挂载和查看
当新介入一个磁盘或者移动硬盘之后，如何使用命令行进行查看。
<!--more-->
## 移动硬盘的使用
移动硬盘在Ubuntu下是没有出现一个类似于windows一样的图标，点击即可进入，那应当如何在命令行中查看呢？或者找到相应的位置然后访问呢？或者让移动硬盘的内容出现在合适的我们希望的地方，我们可以进行访问呢？
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
