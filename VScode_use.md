# 

## 通过官方 PPA 安装 Ubuntu make

    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get install ubuntu-make

## 使用命令安装 visual studio code

    $ umake ide visual-studio-code
    中间会确认安装visual studio code，输入a即可

## 安装完成后，可以发现VSCode图标已经出现在Unity启动器上，点击即可运行。

## 安装报错

    # 若安装完成，图标却没有出现，说明安装错误，报错为
    (process:6655): dconf-WARNING **: failed to commit changes to dconf: Cannot。。。

## 安装报错解决方案

    # 需要重置unity桌面。打开终端（使用快捷键 Ctrl + Alt + F1）进入终端
    # 重置Compiz
    $ dconf reset -f /org/compiz/
    # 重启Unity
    $ setsid unity
    # 如果想重新使用unity默认的启动器图标，可以运行该命令
    $ unity --reset-icons
    # 来重新启动Ubuntu
    $ sudo shutdown -r now

## 卸载已经安装的VSCode

    $ umake ide visual-studio-code  --remove
