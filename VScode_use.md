# Ubuntu16.04 下安装配置 VScode 以及 VS 的使用总结

# 下载及安装

## （1）通过官方 PPA 安装 Ubuntu make

    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get install ubuntu-make

## （2）使用命令安装 visual studio code

    # 中间会确认安装visual studio code，输入a即可
    $ umake ide visual-studio-code

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

    打开VScode  
    ——> 左边栏的EXTENSIONS栏目输入C++  
    ——> 安装C++插件

## （2）建立工程

新建C/C++工程，VScode以文件夹为管理工程的方式，因此需要建立一个文件夹来保存工程。

    新建一个文件夹hello（VScode以文件夹的形式管理工程）  
    ——> 左边栏的EXPLORER栏目打开此文件夹  
    ——> 点击Start中的New file并输入程序新建  
    ——> 右击Untitled-1选择Save  
    ——> 保存为main.cpp文件

## （3）更改配置文件（launch.json）

配置launch.json文件，它是一个启动配置文件。需要进行修改地方的是指定运行的文件，其次我们还可以在里面添加build任务。

    点击左侧的Run按钮  
    ——> create a launch json file  
    ——> 选择C++（GDB/LLDB)  
    ——> 自动生成launch.json文件

修改launch.json文件，参数设置如下：

        // 在生成的默认json文件里需要将program项的内容改为调试时运行的程序  
        "program": "${fileDirname}/${fileBasenameNoExtension}",

改为

        // 指在当前工作文件夹下的main.out文件  
        "program": "${workspaceFolder}/main.out",

## （4）添加构建（编译、链接等）任务（tasks.json）

配置tasks.json文件，这个文件用来方便用户自定义任务，我们可以通过这个文件来添加g++/gcc或者是make命令，方便我们编译程序。

    ctrl+shift+p打开命令行  
    ——> 输入Tasks: Run Task（出现提示：No configured tasks. Configure Tasks...）  
    ——> 回车  
    ——> 选择Create tasks.json file from template  
    ——> 选择Others Example to run an arbitrary external command.  
    ——> 生成默认的tasks.json文件

修改tasks.json文件，参数设置如下：

        {
            // See https://go.microsoft.com/fwlink/?LinkId=733558
            // for the documentation about the tasks.json format
            "version": "2.0.0",
            "tasks": [
                {
                    "label": "build", // label为任务名，将”label"= "echo"改为”label"= "build"
                    "type": "shell",
                    "command": "g++", // 由于我们的指令是g++，这里将”command“=”echo Hello“改为”command“=”g++“
                    "args": ["-g", "${file}"]
                    /*
                    添加g++的参数args；
                    如果我们的g++指令为：g++ -g main.cpp，参数可设置为："args": ["-g", "${file}"]；
                    如果我们想配置g++指令为：g++ -g main.cpp -std=c++11 -o main.out，则参数可设置为："args": ["-g", "${file}", "-std=c++11", "-o", "${fileBasenameNoExtension}.out"]
                    */
                }
            ]
        }

# VScode 运行及调试

上述四个流程完成之后就可以进行基础的C/C++开发与调试了。在进行下面的操作前，我们应当保证launch.json和tasks.json的正确性并且已经成功保存。

    ctrl+shift+p调出命令行  
    ——> Tasks: Run Build Task  
    ——> build  
    ——> Continue without scanning the task output  
    ——> 点击左侧的Run按钮  
    ——> build成功  
    ——> 点击左上角的RUN开始调试（F5是调试也是运行，有断点的时候就是调试，没有断点的时候就是运行）
    Could not find the task 'g++ build active file'.

# 常用快捷键

    ctrl+shift+p：调出命令行
    F5：调试、运行
    Ctrl+shift+B：编译
    F10：单步运行
    F11：进入函数内部
