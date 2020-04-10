# Ubuntu16.04 下安装配置 VScode 以及 VS 的使用总结

# 下载及安装

## 通过官方 PPA 安装 Ubuntu make

    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get install ubuntu-make

## 使用命令安装 visual studio code

    $ umake ide visual-studio-code
    中间会确认安装visual studio code，输入a即可

## 安装完成后，可以发现VSCode图标已经出现在Unity启动器上，点击即可运行。启动器如果没有显示VScode的图标，可以进入刚安装的目录（$ umake ide visual-studio-code步会提醒安装目录），执行“./code"运行，右键鼠标Lock to Launcher即可

# 配置gcc及g++编译器

VScode 不像 codeblock 以及其他编译器那样，有自带的 gcc,g++ 环境，这只是一个编辑器，想要编译需要手动安装 gcc,g++ 编译器，可用如下方法测试是否有 gcc,g++ 编译器：

    # 用一个txt文本，写一个Hello word 的纯c语言代码，保存退出，改名为 hello.c 文件，然后打开终端cd到该.c文件的位置，然后用以下命令编译、运行，如果有Hello word输出则有gcc编译器
    $ gcc -o hello hello.c
    $./ hello

    # 同理，用一个txt文本，写一个Hello word 的纯c++语言代码，保存退出，改名为 hello.cpp文件，然后打开终端cd到该.cpp文件的位置，然后用以下命令编译、运行，如果有Hello word输出则有g++编译器：
    $ gcc -o hello hello.cpp
    $ ./ hello

我的电脑上的问题是g++编译器的确有，不过不能用，需要卸载重新下载，重新安装后终于可以用了。
