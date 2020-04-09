# https://www.ncnynl.com/archives/201704/1535.html

## 
    $ sudo apt-get install ros-kinetic-turtlebot-*
    $ export TURTLEBOT_GAZEBO_WORLD_FILE="/opt/ros/kinetic/share/turtlebot_gazebo/worlds/playground.world"
    $ roslaunch turtlebot_gazebo turtlebot_world.launch
    
    
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
