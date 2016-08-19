---
title: 从一个hector SLAM无法建图的bug开始说起
date: 2016-05-27 02:14:46
tags: hector SLAM
categories: ROS
---
## 某某问:
我使用了Ubuntu 14.04, 安装了Indigo版的ROS,使用了4米搜索半径,240度搜索角度的激光雷达,运行了hector SLAM.然而我在这个长15米,宽3米的走廊上,没办法建图.这么单纯的环境都无法建图,这是为什么啊?

## 某某答:
我们先来了解一下hector slam是如何工作的.
<!--more-->
hector SLAM使用了一个激光雷达,没有测距器.就如同一个人,被蒙上了眼睛,坐在轮椅上.你既看不到周围的环境,也没办法通过轮椅的转动得到自己的运动与否,你只能依靠双手去触摸.
你会依靠双手触摸到的东西去"想象"自己所处的环境。过了一段时间,你再次使用双手去感知周围的环境,摸到了跟上一次摸到的东西一样，你会觉得自己的位置没有改变。而hector SLAM的原理是类似的。
再看回这个场景，LiDAR扫描了一遍，生成一帧图：两边是墙壁，前方没有东西，后面扫不到。下一时刻再扫描一遍，再次得到一帧图片：将这一时刻的图片对比上一时刻的图片，如果两张图片是一样的，hector SLAM会觉得它没有移动，既然没有移动，也就不会进行建图。这就是这个问题的原因。
那么，在这样的特殊环境里面如何建图呢？最好可以从走廊的一端开始建图，然后尽量不要走直线。或者给系统加上别的一些传感器。

> 此文参考于[Robotic的一个问答](http://robotics.stackexchange.com/questions/7387/hector-slam-matching-algorithm)