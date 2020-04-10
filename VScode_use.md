# Ubuntu16.04 下安装配置 VScode 以及 VS 的使用总结

# 下载及安装

## （1）通过官方 PPA 安装 Ubuntu make

    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get install ubuntu-make

## （2）使用命令安装 visual studio code

    $ umake ide visual-studio-code
    中间会确认安装visual studio code，输入a即可

## （3）安装完成后，可以发现VSCode图标已经出现在Unity启动器上，点击即可运行。启动器如果没有显示VScode的图标，可以进入刚安装的目录（$ umake ide visual-studio-code步会提醒安装目录），执行“./code"运行，右键鼠标Lock to Launcher即可

# 配置gcc及g++编译器

VScode 不像 codeblock 以及其他编译器那样，有自带的 gcc,g++ 环境，这只是一个编辑器，想要编译需要手动安装 gcc,g++ 编译器，可用如下方法测试是否有 gcc,g++ 编译器：

    # 用一个txt文本，写一个Hello word 的纯c语言代码，保存退出，改名为 hello.c 文件，然后打开终端cd到该.c文件的位置，然后用以下命令编译、运行，如果有Hello word输出则有gcc编译器
    $ gcc -o hello hello.c
    $./hello

    # 同理，用一个txt文本，写一个Hello word 的纯c++语言代码，保存退出，改名为 hello.cpp文件，然后打开终端cd到该.cpp文件的位置，然后用以下命令编译、运行，如果有Hello word输出则有g++编译器：
    $ gcc -o hello hello.cpp
    $ ./hello

# VScode 环境配置

## （1）安装c/c++插件

打开VScode ——> 左边栏的EXTENSIONS栏目输入C++ ——> 安装C++插件

## （2）建立工程

新建一个文件夹hello（VScode以文件夹的形式管理工程） ——> 左边栏的EXPLORER栏目打开此文件夹 ——> 点击Start中的New file新建main.cpp文件并输入程序

（3）更改配置文件（launch.json）

点击左侧的Debug按钮，选择添加配置（Add configuration）,然后选择C++（GDB/LLDB)，将自动生成launch.json文件，具体操作如下：
生成的默认json文件如下：
注意:这里需要将program项的内容改为调试时运行的程序，将其改为main.out即可。具体更改如下：
            "program": "enter program name, for example ${workspaceFolder}/a.out",
改为
            "program": "${workspaceFolder}/main.out",
该语句指的是当前工作文件夹下的main.out文件，更改完毕的launch.json文件见附录。

（4）添加构建（编译、链接等）任务（tasks.json）

# VScode 运行及调试

F5集是调试也是运行，有断点的时候就是调试没有就是运行..，Ctrl+shift+B编译，另外，F10单步运行，F11进入函数内部，好像还可以运行到某个条件（比如：i==2）。
