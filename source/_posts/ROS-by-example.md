---
title: ROS_by_example
date: 2016-05-13 12:27:24
tags:
categories: ROS
---
# 概念理解
- ROS下的单位和坐标
直角坐标 
![直角坐标](ROS_by_example/coordin.png)
旋转
![旋转](ROS_by_example/rotation.png)
单位：线速度(m/s) 角速度(rad/s) 室内一般不超过0.2m/s
<!--more-->

- odometry
需要记住，无论使用了多少个source，odometry都会与真实的值有差距。

- base controller
包括driver和PID控制器。发布通过/odom frame 到 base frame。某些机器人会使用robot_pose_ekf包对机器人进行更加精确的控制。
有了base controller之后，我们就可以使用ROS提供给我们的命令行工具以及使用ROS的节点发布消息的方式，在一个比较高的层级对对机器人进行控制。我们不再关心这个机器人的使用什么硬件，我们只是单纯的关注机器人在现实中的线速度和角速度的大小，所以只要控ROS的接口即可。

- SLAM package
跟base controller类似，我们也可以在一个较高的层级控制机器人进行建图，只需要我们在ROS环境中添加gmapping package，这个包最好匹配使用激光雷达，也可以使用kinetic和Asus Xtion depth camera。同时，我们可以通过amcl package（Adaptive Monte Carlo Localization）使得机器人能够根据当前的地图信息（current scan）和测量数据（odometry data）自动定位，在地图上点击一个位置，机器人会自动寻路过去并自动避障。

- 架构
![motion control hierachy](ROS_by_example/arci.png)



# 原理理解
# 常用操作
- prepare environment
``` bash
sudo apt-get install ros-indigo-turtlebot-bringup \ros-indigo-turtlebot-create-desktop ros-indigo-openni-* \ros-indigo-openni2-* ros-indigo-freenect-* ros-indigo-usb-cam \ros-indigo-laser-* ros-indigo-hokuyo-node \ros-indigo-audio-common gstreamer0.10-pocketsphinx \ros-indigo-pocketsphinx ros-indigo-slam-gmapping \ros-indigo-joystick-drivers python-rosinstall \ros-indigo-orocos-kdl ros-indigo-python-orocos-kdl \python-setuptools ros-indigo-dynamixel-motor-* \libopencv-dev python-opencv ros-indigo-vision-opencv \ros-indigo-depthimage-to-laserscan ros-indigo-arbotix-* \ros-indigo-turtlebot-teleop ros-indigo-move-base \ros-indigo-map-server ros-indigo-fake-localization \ros-indigo-amcl git subversion mercurial
cd ~/catkin_ws/src
git clone https://github.com/pirobot/rbx1.git$cd rbx1$git checkout indigo-devel
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
rospack profile
udo apt-get install ros-indigo-arbotix-*
sudo apt-get install ros-indigo-laser-* ros-indigo-hokuyo-node
```
- Packages
![packages in rbx](ROS_by_example/files.png)

- Goal
![Goal](ROS_by_example/goal.png)

- First example: helloWorldNavigation_movebase
``` bash
roslaunch rbx1_bringup fake_turtlebot.launch
roslaunch rbx1_nav fake_move_base_blank_map.launch
rosrun rviz rviz -d `rospack find rbx1_nav`/nav.rviz
rostopic pub /move_base_simple/goal geometry_msgs/PoseStamped \'{ header: { frame_id: "map"  }, pose: { position: { x: 1.0, y: 0, z: 0  }, orientation: { x: 0, y: 0, z: 0, w: 1  }  }  }'
rosstopic pub /move_base_simple/goal geometry_msgs/PoseStamped \'{ header: { frame_id: "map"  }, pose: { position: { x: 0, y: 0, z: 0  }, orientation: { x: 0, y: 0, z: 0, w: 1  }  }  }''
```
Point And Click:使用鼠标点击左下角的reset按钮可以清除之前的轨迹，再点击右上方的2D Nav Goal按钮，就可以使用鼠标再地图上指定目标。
<iframe height=498 width=510 src="http://player.youku.com/embed/XMTU3Njk1Nzc0OA==" frameborder=0 allowfullscreen></iframe>

- Second example: helloWorldNavigation_AvoidingObstacles
``` bash
roslaunch rbx1_bringup fake_turtlebot.launch
rosparam delete /move_base
roslaunch rbx1_nav fake_move_base_map_with_obstacles.launch
rosrun rviz rviz -d `rospack find rbx1_nav`/nav_obstacles.rviz
rosrun rbx1_nav move_base_square.py
```
<iframe height=498 width=510 src="http://player.youku.com/embed/XMTU3Nzg2Njk2NA==" frameborder=0 allowfullscreen></iframe>

- Third example: helloWorldGmapping
``` bash
roslaunch rbx1_bringup turtlebot_minimal_create.launch
rosrun rviz rviz -d `rospack find rbx1_nav`/fake_laser.rviz
```

- Fourth example: helloWorldGmapping_record&create
``` bash
roslaunch rbx1_bringup turtlebot_minimal_create.launch
roslaunch rbx1_nav gmapping_demo.launch
rosrun rviz rviz -d `rospack find rbx1_nav`/gmapping.rviz
roslaunch rbx1_nav keyboard_teleop.launch
roscd rbx1_nav/bag_files
rosbag record -O my_scan_data /scan /tf
rosrun map_server map_saver -f my_map
```
备注：对于大量数据的时候，使用use_sim_time控制
``` bash
rosparam set use_sim_time true
rosparam set use_sim_time false
```
- Fifth example: helloWorldAmcl
``` bash
roslaunch rbx1_bringup fake_turtlebot.launch
roslaunch rbx1_nav fake_amcl.launch map:=test_map.yaml
rosrun rviz rviz -d `rospack find rbx1_nav`/amcl.rviz
```
<iframe height=498 width=510 src="http://player.youku.com/embed/XMTU3Nzg1OTc5Mg==" frameborder=0 allowfullscreen></iframe>

# 问题解决
## 在新终端下没有进行source
- Testing the Simulator出现的现象
运行：
``` bash
roslaunch rbx1_bringup fake_turtlebot.launch
rosrun rviz rviz -d `rospack find rbx1_nav`/sim.rviz
```
看到的是：
![turtlebot](ROS_by_example/ar_roboct.png)
![rviz](ROS_by_example/sim_rviz.png)
可以看到，并没有出现预期会存在的机器人。
- 分析
看到命令行中使用了rospack find，所以可以想到应该是需要source才行，所以，运行了
``` bash
source ~/catkin_ws/devel/setup.bash
```
再重复上述之前的两条，可以得到正确的运行。
![小龟](ROS_by_example/ar_roboct_true.png)
![溜一下小龟](ROS_by_example/trunaround_ar_rob.png)
