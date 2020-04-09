# https://www.ncnynl.com/archives/201609/787.html

## 
    $ sudo apt-get install ros-kinetic-turtlebot-*
    $ export TURTLEBOT_GAZEBO_WORLD_FILE="/opt/ros/kinetic/share/turtlebot_gazebo/worlds/playground.world"
    $ roslaunch turtlebot_gazebo turtlebot_world.launch

上网本：放在turtlebot上（主机，IP：192.168.0.121，计算机名：FriendlyELEC）  
工作站：用于处理计算及rviz图形，三维可视化工具使用（从机，IP：192.168.43.6，计算机名：）  
路由器：允许工作站和turtlebot通过本地IP通信
    
## 硬件 

Kobuki底盘  
激光雷达EAI S2

## 软件
主机端：  
ubuntu 16.04  
ROS kinetic

从机端：  

主从端SLAM：  
Gmapping：https://github.com/ros-perception/openslam_gmapping.git  
hector_slam：https://github.com/tu-darmstadt-ros-pkg/hector_slam.git  
cartographer：https://github.com/googlecartographer/cartographer.git  
slam_karto：https://github.com/ros-perception/slam_karto.git  

## 配置网络

（1）分别在两台计算机系统 /etc/hosts 文件中加入对方的 IP 地址和计算机名  
192.168.0.121 FriendlyELEC  
192.168.43.6

（2）从机设置 ROS_MASTER_URI  
echo "export ROS_MASTER_URI=http://FriendlyELEC:11311" >> ~/.bashrc
