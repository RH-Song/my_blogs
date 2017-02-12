---
title: 安装ROS Indigo 
categories: ROS
date: 2016-05-03 19:12:03
tags: Indigo 
---

# 安装
## 版本以及系统
ROS为LTS版本Indigo，系统为64位Ubuntu 14.04。
## 安装过程
- follow 官网上的 [Install](http://wiki.ros.org/ROS/Installation)
- 备注：这个过程比较漫长（我在follow了这个Install之后，耗时3个多小时，如果你的网络比较好，可能会跟快），如果不行的话，请尝试更换安装的镜像的源。如果还不行，可以考虑换个时间再搞，说不定是当时某个网络故障导致的。如果依然不行，可以尝试更换系统。我尝试过64位的Ubuntu16.04以及32位的Ubuntu14.04，最后才选择了64位的Ubuntu14.04，这个系统基本可以自动解决依赖的问题，当然折腾另外连个系统的时间没有算在3个小时里面。
<!--more-->
# StartGuide
## ROS学习
两个途径可选
- [Tutorial](http://wiki.ros.org/cn/ROS/Tutorials)
- [Overview](http://wiki.ros.org/cn/ROS/Introduction)
关于架构的东西，可以参考[ROS核心文档](http://wiki.ros.org/ROS)
## Answer
提供三个途径搜索不知道的问题的答案。
- 使用官网页面的Search功能
- [FAQ1](http://answers.ros.org/questions/)
- [FAQ2](http://code.ros.org/lurker/list/ros-users.html)
## 代码
可以在这个[代码浏览处](http://www.ros.org/browse/list.php)查看。

# 附上安装过程的截图
- ros-indigo安装完成的截图
![indigo install finish](ROS_install_indigo/finish.png)
- 安装rosdep的图
![rosdep](ROS_install_indigo/rosdep.png)
- 完成最后一步安装
![rosinstall](ROS_install_indigo/build.png)
