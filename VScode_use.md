# Ubuntu16.04 下安装配置 VScode 以及 VS 的使用总结

## 通过官方 PPA 安装 Ubuntu make

    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get install ubuntu-make

## 使用命令安装 visual studio code

    $ umake ide visual-studio-code
    中间会确认安装visual studio code，输入a即可

## 安装完成后，可以发现VSCode图标已经出现在Unity启动器上，点击即可运行。启动器如果没有显示VScode的图标，可以进入刚安装的目录（$ umake ide visual-studio-code步会提醒安装目录），执行“./code"运行，右键鼠标Lock to Launcher即可
