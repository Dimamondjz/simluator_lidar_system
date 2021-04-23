# 差速无人车16线velodyne激光雷达仿真平台

##### Author :Zhen_jia

##### Date: 2021.4.23

## 1.适配环境:

#### 	ubuntu 18.04 +Ros-melodic+Gazebo+ cpp14以上版本(gcc>=5.5,g++>=5.5,camke>=3.1.3)

​	安装 [Ros-mdelodic full desktop](http://wiki.ros.org/melodic/Installation)

​		 [Husky official package](http://wiki.ros.org/husky_gazebo/Tutorials/Simulating%20Husky)

​		 ROS-grid_map package 安装命令:

​	`sudo apt-get install ros-melodic-grid-map`

​		 ROS-melodic move base package 安装命令:

​	`sudo apt-get install ros-melodic-navigation`

​		 ROS-Gazebo  安装命令:

​	`sudo apt install ros-melodic-gazebo9*`

​		ROS-Gazebo的坑

​		1.1出现gazebo 报错 [Err] [REST.cc:205] Error in REST request 解决 或者url的问题需要修改：

`		gedit .ignition/fuel/config.yaml`

​		将

​		url: [https://api.ignitionfuel.org](https://api.ignitionfuel.org/)

​		改为

​		url: https://api.ignitionrobotics.org

​		**注意：**一定要对齐 url 与name对齐

​		1.2当gazebo开启时出现长时间黑屏或raparing .....时，因为需要下载模型且模型较大可[下载模型](https://github.com/osrf/gazebo_models)

​		https://github.com/osrf/gazebo_models

​		随后将里面的众多文件夹解压至

​		/home/用户名/.gazebo/models

## 2.检查环境依赖:

###### 	在src所在的目录下执行

​	`rosdep install --from-path src --ignore-src --rosdistro=melodic -y`

## 3.安装编译:

​	3.1在src所在的目录下执行

​	`catkin_make -DCMAKE_BUILD_TYPE=Release`

​	3.2添加环境变量

​	`gedit ~/.bashrc `

​	`export HUSKY_URDF_EXTRAS=$(rospack find husky_custom_description)/urdf/custom_description.urdf.xacro`

​	此时应该有两个环境变量在~/.bashrc的下方

​	`export HUSKY_GAZEBO_DESCRIPTION=$(rospack find husky_gazebo)/urdf/description.gazebo.xacro`
​	`export HUSKY_URDF_EXTRAS=$(rospack find husky_custom_description)/urdf/custom_description.urdf.xacro`

​	3.3如果为了方便可以将下方加入~/.bashrc

​	`source /home/所在文件夹..../devel/setup.bash`

​	并执行下方立刻加载修改后的设置

​	`	source ~/.bashrc `

##  4.启动:

​	4.1启动gazebo

​	`roslaunch husky_gazebo husky_playpen.launch`

​	4.2启动显示rviz

​	`roslaunch husky_viz view_robot.launch`

​	4.3启动loam用于SLAM (mapping and location robot)

​	`roslaunch loam_velodyne loam_velodyne.launch`

​	4.4启动用于几何信息和地图传递

​	`roslaunch topo_confidence_map mapping.launch`

​	4.5启动用于将导航目标传递

​	`roslaunch husky_navigation_goals send_goal.launch `

若有其他问题可以看原版14.04和16.04的[readme](https://github.com/Dimamondjz/Autonomous-Outdoor-Scanning-via-Online-Topological-and-Geometric-Path-Optimization)
