# SLAM环境配置：Linux+Clion+Eigen+Ceres+g2o+Sophus+PCL+OpenCV+测试代码


# ubuntu16.04+eigen3 安装

    # eigen头文件默认位置/usr/include/eigen3，可用如下命令查找位置：
    $ sudo updatedb
    $ locate eigen3
    
    # apt-get方式安装
    $ sudo apt-get install libeigen3-dev

    # 因为eigen3被默认安装到了usr/include里了（或者是usr/local/include里，这两个都差不多，都是系统默认的路径），
    但在很多程序中include时经常使用 #include <Eigen/Dense>而不是使用#include <eigen3/Eigen/Dense>，
    所以要将usr/include/eigen3文件夹中的Eigen文件递归地复制到上一层文件夹，否则一些程序在编译时会因找不到Eigen/Dense而报错，
    那就只能在CMakeLists.txt用include_libraries(绝对路径了)。
    $ sudo cp -r /usr/include/eigen3/Eigen /usr/include
    
# eigen3 测试代码
main.cpp

    #include <iostream>
    #include <cmath>
    using namespace std;

    #include <Eigen/Core>
    // Eigen 几何模块
    #include <Eigen/Geometry>

    /****************************
    * 本程序演示了 Eigen 几何模块的使用方法
    ****************************/

    int main ( int argc, char** argv )
    {
        // Eigen/Geometry 模块提供了各种旋转和平移的表示
        // 3D 旋转矩阵直接使用 Matrix3d 或 Matrix3f
        Eigen::Matrix3d rotation_matrix = Eigen::Matrix3d::Identity();
        // 旋转向量使用 AngleAxis, 它底层不直接是Matrix，但运算可以当作矩阵（因为重载了运算符）
        Eigen::AngleAxisd rotation_vector ( M_PI/4, Eigen::Vector3d ( 0,0,1 ) );     //沿 Z 轴旋转 45 度
        cout .precision(3);
        cout<<"rotation matrix =\n"<<rotation_vector.matrix() <<endl;                //用matrix()转换成矩阵
        // 也可以直接赋值
        rotation_matrix = rotation_vector.toRotationMatrix();
        // 用 AngleAxis 可以进行坐标变换
        Eigen::Vector3d v ( 1,0,0 );
        Eigen::Vector3d v_rotated = rotation_vector * v;
        cout<<"(1,0,0) after rotation = "<<v_rotated.transpose()<<endl;
        // 或者用旋转矩阵
        v_rotated = rotation_matrix * v;
        cout<<"(1,0,0) after rotation = "<<v_rotated.transpose()<<endl;

        // 欧拉角: 可以将旋转矩阵直接转换成欧拉角
        Eigen::Vector3d euler_angles = rotation_matrix.eulerAngles ( 2,1,0 ); // ZYX顺序，即roll pitch yaw顺序
        cout<<"yaw pitch roll = "<<euler_angles.transpose()<<endl;

        // 欧氏变换矩阵使用 Eigen::Isometry
        Eigen::Isometry3d T=Eigen::Isometry3d::Identity();                // 虽然称为3d，实质上是4＊4的矩阵
        T.rotate ( rotation_vector );                                     // 按照rotation_vector进行旋转
        T.pretranslate ( Eigen::Vector3d ( 1,3,4 ) );                     // 把平移向量设成(1,3,4)
        cout << "Transform matrix = \n" << T.matrix() <<endl;

        // 用变换矩阵进行坐标变换
        Eigen::Vector3d v_transformed = T*v;                              // 相当于R*v+t
        cout<<"v tranformed = "<<v_transformed.transpose()<<endl;

        // 对于仿射和射影变换，使用 Eigen::Affine3d 和 Eigen::Projective3d 即可，略

        // 四元数
        // 可以直接把AngleAxis赋值给四元数，反之亦然
        Eigen::Quaterniond q = Eigen::Quaterniond ( rotation_vector );
        cout<<"quaternion = \n"<<q.coeffs() <<endl;   // 请注意coeffs的顺序是(x,y,z,w),w为实部，前三者为虚部
        // 也可以把旋转矩阵赋给它
        q = Eigen::Quaterniond ( rotation_matrix );
        cout<<"quaternion = \n"<<q.coeffs() <<endl;
        // 使用四元数旋转一个向量，使用重载的乘法即可
        v_rotated = q*v; // 注意数学上是qvq^{-1}
        cout<<"(1,0,0) after rotation = "<<v_rotated.transpose()<<endl;

        return 0;
    }
    
CMakeLists.txt

    cmake_minimum_required(VERSION 3.14)
    project(eigen_test)

    set(CMAKE_CXX_STANDARD 14)

    include_directories("/usr/include/eigen3")

    add_executable(eigen_test main.cpp)

测试

    # mkdir build
    # cd build
    # cmake ..
    # make
    
    # ./eigen_test
