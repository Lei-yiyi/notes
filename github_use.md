# 使用终端命令行将本地项目上传到 Github 并提交代码

## （1）在 Github 上创建自己的 repository

## （2）建立本地仓库 cd 到你的本地项目根目录下，执行 git 命令

    $ cd 到你的项目目录下
    $ git init
    
    # 取消对文件夹 git init 初始化操作并查看    
    $ rm -rf .git/    
    $ ls -a

## （3）将本地项目工作区的所有文件添加到暂存区

    $ git add . 

## （4）将暂存区的文件提交到本地仓库

    $ git commit -m "注释"
    
    # 首次上传GitHub，接着输入以下命令，邮箱和用户名就是注册GitHub时的
    $ git config --global user.email "自己的邮箱"
    $ git config --global user.name "用户名"

## （5）将本地仓库关联到Github上

    $ git remote add origin 自己的url（创建的仓库的地址，赋值地址栏里面的地址即可，如 https://github.com/zhibinhsu/ShowAllLabel.git ）

    # 如果提示错误：fatal: remote origin already exists. 解决办法如下（先删除远程 Git 仓库，再重新添加远程 Git 仓库）：
    $ git remote rm origin 
    $ git remote add origin 自己的url（创建的仓库的地址，赋值地址栏里面的地址即可，如 https://github.com/zhibinhsu/ShowAllLabel.git ）

## （6）同步到服务器

    $ git push -u origin master
    
    # 如果提示错误：error: failed to push some refs to,具体错误信息如下：  
    To https://github.com/zhanglei995/slam_test.git
    ! [rejected]        master -> master (fetch first)
    error: failed to push some refs to 'https://github.com/zhanglei995/slam_test.git'
    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
    
    先将本地和远程的文件合并后，再上传本地的新文件
    $ git pull origin master
    $ git push -u origin master

## （7）常用操作

    # 查看状态
    $ git status
    
    # 克隆远程仓库，单击绿色的按钮Clone or download，然后点击复制链接
    $ git clone 复制的链接（远程地址）
    
    # fetch是将远程主机的最新内容拉到本地，不进行合并
    $ git fetch origin master
    
    # pull是将远程主机的master分支最新内容拉下来后与当前本地分支直接合并 fetch+merge
    $ git pull origin master
    
    # 查看本地和远程的所有分支
    $ git branch -a
    
    # 查看远程所有分支
    $ git branch -r
    
    # 删除缓存区所有文件
    $ git rm -r --cached .
