# mrpt 使用

## （1）查看 ubuntu 和 ROS 的版本

查看 ubuntu 的版本：$ lsb_release -a  
查看 ROS 的版本：$ roscore

## （2）mrpt相关资源网站

http://www.mrpt.org/  
https://github.com/mrpt-ros-pkg/  
http://wiki.ros.org/mrpt_navigation  
http://wiki.ros.org/mrpt_slam

## （3）http://wiki.ros.org/mrpt_navigation （Build from sources）

    # 安装 ROS（ubuntu 版本为 Ubuntu 16.04，ROS 版本为kinetic）  

    # 编译/安装 MRPT（选择从官方 Debian / Ubuntu 存储库安装 MRPT）  
    $ sudo apt-get install libmrpt-dev  

    # 在 catkin 工作区中克隆此存储库（此处工作区为 mrpt_ws）  
    $ mkdir -p ~/mrpt_ws/src  
    $ cd ~/mrpt_ws/src  
    $ git clone https://github.com/mrpt-ros-pkg/mrpt_navigation.git  
    $ cd ..  
    $ catkin_make  

    # 运行单元测试  
    $ catkin_make run_tests  

    # 配置环境变量  
    $ echo "source ~/mrpt_ws/devel/setup.bash" >>  ~/.bashrc  
    $ source ~/.bashrc

    # Demos（http://wiki.ros.org/mrpt_localization）  
    $ roslaunch mrpt_localization demo.launch

### catkin_make 报错信息1

    CMake Error at /opt/ros/kinetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
      Could not find a package configuration file provided by "mrpt_bridge" with
      any of the following names:

        mrpt_bridgeConfig.cmake
        mrpt_bridge-config.cmake

      Add the installation prefix of "mrpt_bridge" to CMAKE_PREFIX_PATH or set
      "mrpt_bridge_DIR" to a directory containing one of the above files.  If
      "mrpt_bridge" provides a separate development package or SDK, be sure it
      has been installed.
    Call Stack (most recent call first):
      mrpt_navigation/mrpt_local_obstacles/CMakeLists.txt:7 (find_package)


    -- Configuring incomplete, errors occurred!
    See also "/home/pi/mrpt_ws/build/CMakeFiles/CMakeOutput.log".
    See also "/home/pi/mrpt_ws/build/CMakeFiles/CMakeError.log".

### catkin_make 报错信息1解决方法

    $ sudo apt-get install ros-kinetic-mrpt-bridge

### catkin_make 报错信息2

    CMake Error at /opt/ros/kinetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
      Could not find a package configuration file provided by "pose_cov_ops" with
      any of the following names:

        pose_cov_opsConfig.cmake
        pose_cov_ops-config.cmake

      Add the installation prefix of "pose_cov_ops" to CMAKE_PREFIX_PATH or set
      "pose_cov_ops_DIR" to a directory containing one of the above files.  If
      "pose_cov_ops" provides a separate development package or SDK, be sure it
      has been installed.
    Call Stack (most recent call first):
      mrpt_navigation/mrpt_localization/CMakeLists.txt:7 (find_package)


    -- Configuring incomplete, errors occurred!
    See also "/home/pi/mrpt_ws/build/CMakeFiles/CMakeOutput.log".
    See also "/home/pi/mrpt_ws/build/CMakeFiles/CMakeError.log".
    Invoking "cmake" failed

### catkin_make 报错信息2解决方法

    $ sudo apt-get install ros-kinetic-pose-cov-ops

## （4）http://wiki.ros.org/mrpt_slam （Build from sources）

    # 安装 ROS（ubuntu 版本为 Ubuntu 16.04，ROS 版本为kinetic）  

    # 编译/安装 MRPT（选择从官方 Debian / Ubuntu 存储库安装 MRPT）  
    $ sudo apt-get install libmrpt-dev  

    # 在 catkin 工作区中克隆此存储库（此处工作区为 mrpt_ws）  
    $ mkdir -p ~/mrptSLAM_ws/src  
    $ cd ~/mrptSLAM_ws/src  
    $ git clone https://github.com/mrpt-ros-pkg/mrpt_slam.git  
    $ cd ..  
    $ catkin_make  

    # 运行单元测试  
    $ catkin_make run_tests  

    # 配置环境变量  
    $ echo "source ~/mrptSLAM_ws/devel/setup.bash" >>  ~/.bashrc  
    $ source ~/.bashrc

    # Demos（http://wiki.ros.org/mrpt_ekf_slam_2d）  
    $ roslaunch mrpt_ekf_slam_2d ekf_slam_2d.launch

### catkin_make 报错信息3

    CMake Error at /opt/ros/kinetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
      Could not find a package configuration file provided by
      "multimaster_msgs_fkie" with any of the following names:

        multimaster_msgs_fkieConfig.cmake
        multimaster_msgs_fkie-config.cmake

      Add the installation prefix of "multimaster_msgs_fkie" to CMAKE_PREFIX_PATH
      or set "multimaster_msgs_fkie_DIR" to a directory containing one of the
      above files.  If "multimaster_msgs_fkie" provides a separate development
      package or SDK, be sure it has been installed.
    Call Stack (most recent call first):
      mrpt_slam/mrpt_graphslam_2d/CMakeLists.txt:9 (find_package)


    -- Configuring incomplete, errors occurred!
    See also "/home/pi/mrptSLAM_ws/build/CMakeFiles/CMakeOutput.log".
    See also "/home/pi/mrptSLAM_ws/build/CMakeFiles/CMakeError.log".
    Invoking "cmake" failed

### catkin_make 报错信息3解决方法

    $ sudo apt-get install ros-kinetic-multimaster-msgs-fkie

### roslaunch mrpt_ekf_slam_2d ekf_slam_2d.launch 报错信息1

    ERROR: unable to contact ROS master at [http://:11311]
    The traceback for the exception was written to the log file

### roslaunch mrpt_ekf_slam_2d ekf_slam_2d.launch 报错信息1解决方法

    # 打开一个终端，打开 roscore
    $ roscore  
    
    # 再打开一个终端，继续运行Demos
    $ roslaunch mrpt_ekf_slam_2d ekf_slam_2d.launch
