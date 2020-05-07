说明：
1、包robot_sim_demo：（必需）
	提供gazebo仿真需要的机器人模型、世界模型、配置文件
2、包vel_pkg：（自定义）
	wpb_home_velocity_control.cpp:沿x轴向前运动
	wpb_home_behavior_node.cpp:通过激光雷达简单避障
3、在自己的程序仿真时候，保留包1，替换包2即可。



步骤：
1、打开一个cmd，到home目录下，
	$ mkdir -p demo_ws/src
2、将文件夹中的两个文件复制到src目录下
3、到demo_ws目录
	$ rosdep install --from-paths src --ignore-src	--rosdistro=kinetic	-y
	$ catkin_make 
	$ source ./devel/setup.bash
	$ roslaunch robot_sim_demo robot_spawn.launch
4、打开另一个cmd，到demo_ws目录
	$ source ./devel/setup.bash
	$ rosrun vel_pkg wpb_home_velocity_control
	$ rosrun vel_pkg wpb_home_behavior_node



注意：
1、在开始编译之前，需要确保Gazebo在7.0版本以上
	$ gazebo -v	#确认7.0及以上
  如果你的Gazebo版本低于7.0，则需要进行升级
	$ sudo sh -c echo "deb	http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_re lease -cs` main"	> /etc/apt/sources.list.d/gazebo-stable.list' 
	$ wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add
	$ sudo apt-get update 
	$ sudo apt-get install gazebo7
2、可以使用rostopic list查看话题

