---
title: ros_tutorial
date: 2016-05-03 22:12:18
tags: 
categories: ROS
---

# 前言
这篇文章在于记录我学习ros初级教程，算是个人的一个总结，如果您需要了解全部的教程，请直接访问官方[tutorial](http://wiki.ros.org/ROS/Tutorials)，里面讲解很详细，称得上是手把手教学。
<!--more-->
# 初级教程
## 安装并配置ROS环境
### 安装
根据installation进行
### 管理环境
检测是否配置好环境变量
``` bash
export | grep ROS
```
### 创建ROS工作空间
- 创建catkin工作空间
``` bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
```
- 刚建立为空，也可以进行编译
``` bash
cd ~/catkin_ws
catkin_make
```
编译之后得到
![catkin_make](ros_tutorial/catkin_make.png)

一个需要的命令行：
``` bash
source ./devel/setup.bash
```
### ROS文件系统介绍
ROS文件系统是有package组成，里面会包含各种源码，脚本等等。同时，Manifest是以package.xml表现，描述各个package之间的依赖关系。
与文件系统相关的命令行工具：
- rospack 
- roscd
- rosls
- 使用tab
以上命令的意义跟Linux中去掉ros之后的命令非常像，比如roscd跟cd的意义很想，只是roscd可以直接cd到ros相关的目录下。
### ROS程序包
这个程序包需要的架构大致如下：
![package structure](ros_tutorial/package.png)
以上的架构希望可以记住在心中，因为后面在尝试自己构建的程序包的时候，是很基本的概念。
包的依赖可以分为一级依赖和间接依赖,依赖项分为build_depend、buildtool_depend、run_depend、test_depend。查看依赖包可以使用
``` bash
rospack depends1 [程序包]
```
创建程序包之后，可以使用catkin_make进行编译。
### 理解ROS节点
首先了解一下概念：
- Nodes:节点,一个节点即为一个可执行文件，它可以通过ROS与其它节点进行通信。
- Messages:消息，消息是一种ROS数据类型，用于订阅或发布到一个话题。
- Topics:话题,节点可以发布消息到话题，也可以订阅话题以接收消息
- Master:节点管理器，ROS名称服务 (比如帮助节点找到彼此)
- rosout: ROS中相当于stdout/stderr。
- roscore: 主机（Master）+ rosout + 参数服务器 (参数服务器会在后面介绍)
- 客户端库：可以是Python也可以是C++。可以允许使用不同编程语言的节点进行通信。
接下来看到roscore，在上面的概念中提到的，它包括主机，输出以及参数服务器，所以它会包含一个比较特殊的node（节点），输出，同时它需要在运行所有ROS程序之前先运行。
关于ROS节点可以使用的命令行工具可以有：
- roscore
- rosnode
- rosrun
### ROS话题
ROS节点是通过话题相互通信。而这种通信是通过发送消息（messages）实现。使用messages注意发布的数据类型必须相同。尝试使用rostopic pub进行广播的话题。
### ROS服务与参数
服务（services）是节点之间通讯的另一种方式。服务允许节点发送请求（request）并获得一个响应（response）。rosservice可以很轻松的使用 ROS 客户端/服务器框架提供的服务。rosservice提供了很多可以在topic上使用的命令：
- rosservice list         输出可用服务的信息
- rosservice call         调用带参数的服务
- rosservice type         输出服务类型
- rosservice find         依据类型寻找服务find services by service type
- rosservice uri          输出服务的ROSRPC uri
以上指令后面可以带出一系列命令。比如：rosservice list clear。
参数可以是整型、浮点、布尔、字符串、字典和列表等数据类型。参数可以使用：rosparam进行操作：
- rosparam set            设置参数
- rosparam get            获取参数
- rosparam load           从文件读取参数
- rosparam dump           向文件中写入参数
- rosparam delete         删除参数
- rosparam list           列出参数名
### 使用 rqt_console 和 roslaunch
这两个是非常有用的工具。
- rqt_console属于ROS日志框架(logging framework)的一部分，用来显示节点的输出信息。rqt_logger_level允许我们修改节点运行时输出信息的日志等级（logger levels）（包括 DEBUG、WARN、INFO和ERROR）。
- roslaunch可以用来启动定义在launch文件中的多个节点。
``` bash
roslaunch [package] [filename.launch]
```
### 创建消息和服务
- 消息(msg): msg文件就是一个描述ROS中所使用消息类型的简单文本。它们会被用来生成不同语言的源代码。msg文件存放在package的msg目录下。
- 服务(srv): 一个srv文件描述一项服务。它包含两个部分：请求和响应。srv文件则存放在srv目录下。
上面提到过，消息使用相同的数据类型。消息的数据类型可以有哪些呢？可以包含：
- int8, int16, int32, int64 (plus uint*)
- float32, float64
- string
- time, duration
- other msg files
- variable-length array[] and fixed-length array[C]
还有一个特殊的数据类型：Header。而在msg文件中，每一行都包含一个：类型以及变量名。
```
Header header
string child_frame_id
geometry_msgs/PoseWithCovariance pose
geometry_msgs/TwistWithCovariance twist
```

而对于srv文件，则是分为请求和响应两部分，由'---'分隔。   
``` 
int64 A
int64 B
---
int64 Sum
```
在使用的时候需要相应的修改package.xml以及CMakelists.txt。
### 编写消息发布器以及订阅器（使用官网上的一个例子）
在src文件夹下，新建发布器[talker](https://raw.github.com/ros/ros_tutorials/groovy-devel/roscpp_tutorials/talker/talker.cpp)以及订阅器[listener](https://raw.github.com/ros/ros_tutorials/groovy-devel/roscpp_tutorials/listener/listener.cpp) 并且相应的修改[CMakelists.txt](https://raw.github.com/ros/catkin_tutorials/master/create_package_pubsub/catkin_ws/src/beginner_tutorials/CMakeLists.txt) （点击可以查看源代码）
编译运行之后，可以看到效果：
![talker](ros_tutorial/talker.png)
![listener](ros_tutorial/listener.png) 

### 编写service和client（使用官网上的一个例子）
在src中添加add_two_ints_server.cpp和add_two_ints_client.cpp，可以在官网查看[源代码](http://wiki.ros.org/cn/ROS/Tutorials/WritingServiceClient%28c%2B%2B%29)
编译运行之后，可以得到：
![service](ros_tutorial/servier.png)
![client](ros_tutorial/client.png)
## 至此
至此，对于ROS当中一些非常基本的概念以及关系已经了解了。之后还可以结合我在Start Guide这篇blog中提到的途径进行进一步的学习。

# 关于一只龟的故事
在tutorial中有一只关于龟的模拟。
- 开启







	
