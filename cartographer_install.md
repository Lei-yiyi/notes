# cartographer 安装

ubuntu 16.04 ROS kinetic  

ubuntu版本：16.04  
ROS版本：kinetic  
源码编译过程中会占用大量内存，保证：真实内存+swap > 4G  
查看方法：$ free -m  

## （1）安装依赖

$ sudo apt-get install -y google-mock libboost-all-dev libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx ros-kinetic-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev

cartographer是基于ceres solver和protobuf开发的。

## （2）安装ceres solver

$ git clone https://github.com/hitcm/ceres-solver-1.11.0.git  
$ cd ceres-solver-1.11.0  
$ mkdir build && cd build  
$ cmake .. && make && sudo make install  

cartographer编译过程中检测到ceres solver没有安装，会自动去国外网站下载，速度特别慢，所以我们自己先安装好。

## （3）升级protoc3

$ git clone https://github.com/protocolbuffers/protobuf.git  
$ cd protobuf  
$ ./autogen.sh  
$ ./configure  
$ make  && sudo make install  
$ sudo ldconfig # refresh shared library cache.

ubuntu16.04的protobuf的版本默认是2.x ，但是cartographer要求是3.0以上，所以我们要从源码去升级protobuf。

执行./autogen.sh过程中很有可能会出现以下错误提示：  
./autogen.sh: autoreconf: not found  
解决办法：  
$ sudo apt-get install autoconf  
$ sudo apt-get install automake  
$ sudo apt-get install libtool  

## （4）安装cartographer

$ git clone https://github.com/googlecartographer/cartographer.git  
$ cd cartographer && mkdir build && cd build  
$ cmake .. && make && sudo make install  

使用官方网址：https://github.com/googlecartographer/cartographer.git ，避免后面遇到文件缺失问题。

## （5）安装cartographer_ros

初始化工作空间  
$ mkdir -p catkin_google_ws/src  
$ cd catkin_google_ws/src  
$ catkin_init_workspace  

安装cartographer_ros  
$ cd catkin_google_ws/src  
$ git clone https://github.com/googlecartographer/cartographer_ros.git  
$ cd ..  
$ catkin_make

添加工作空间  
$ echo "source ~/catkin_google_ws/devel/setup.bash" >> ~/.bashrc  
$ source ~/.bashrc  

执行catkin_init_workspace过程中很有可能会出现以下错误提示：  
The program 'catkin_init_workspace' is currently not installed. You can install it by typing:  
sudo apt install catkin  
解决办法：  
$ source /opt/ros/kinetic/setup.bash
