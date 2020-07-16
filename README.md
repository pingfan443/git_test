# 练习git命令

# git学习资源

[传送门](https://www.bilibili.com/video/BV1sJ411D7xN?p=7)

# git安装

git安装教程：
[传送门](https://blog.csdn.net/sanxd/article/details/82624127?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
如果发现git在cmd中输入git找不到命令是因为没有配置环境变量，需要自己配置环境静变量（附带教程：[传送门](https://www.cnblogs.com/-mrl/p/11246666.html)）另外这个其实也不需要一定要配置，也可以直接在git bash中直接运行即可。


# 本地仓库操作

## 安装好后需要进行全局配置

```c++
git config --global user.name "pingfan443"
git config --global user.email "pingfan23@foxmail.com"
    /*
    查看用户名有没有问题
    	git config --global user.name
    查看邮箱有没有问题
    	git config --global user.email
    */
```

## 练习命令

在git界面创建文件夹(默认桌面，可修改)
    `mkdir git_first`
打开这个文件夹(tab键可以提示)
    `cd git_first`
初始化git仓库(会有一个.git文件夹，隐藏的需要设置成打开隐藏项目)
    `git init`	  
    (这个是初始化一个仓库，然后自己可以写东西，上传到远程仓库)

## git常用指令操作


查看当前状态：
`git status`

添加到缓存区：
git add 文件名

说明：git add  指令可以添加一个或者多个文件

1: `git add 文件名`

2：`git add 文件名1 文件名2···`

3：`git add . 	添加当前目录到缓存区中`

提交至版本库：

`git commit -m "注释内容"`



## 版本控制

1查看版本：

`git log`

`git log --pretty=online`

2回退操作（比如先后创建了三个文件，你想回到创建第一个文件的时刻）

指令：`git reset --hard 提交编号`



# 远程仓库

首先是在github上创建仓库

两种常规使用方式

## 基于http协议

将仓库克隆到本地

`git clone 线上仓库地址`
（记住是http）
例如：
git clone `https://github.com/pingfan443/git_test.git`

在仓库上做对应的操作（提交缓存区，提交本地仓库，提交线上仓库，拉取线上仓库）

提交缓存区

`git add algotithm.md`	添加algotithm.md文件

`git commit -m "对文件的注释"`

提交到线上仓库的指令：

`git push`

新版本会直接提示一个用户名和密码窗口，直接输入就可以上传到仓库中去

由于是http协议，他不会记住你的密码，所以你每次提交都会输入用户名和密码，解决办法：

在本地仓库中找到config文件打开修改url

`用户名:密码@`

url = https://用户名:密码@github.com/pingfan443/git_test.git


拉取线上仓库：git pull(当别人上传文件之后第二天你需要进行实时更新到你的本地仓库)

## 基于ssh协议

生成公私钥对指令（）：`ssh-keygen -t rsa -C "注册邮箱"`		后边一路回车即可

### new公钥的方法

1：找到里边的公钥（your public ····）在c/user/用户名/.ssh/id_rsa.pub复制下来，去github上打开setting找到ssh and gpg keys  然后  new一个ssh名字随意起，然后把赋值的放进去点击下边的创建即可。

2：执行`cat ~/.ssh/id_rsa.pub	`	之后会产生一个文件，复制下来，去github上setting下....操作同1

验证上传公钥成功方法：

执行：`ssh -T git@github.com`

`Hi pingfan443! You've successfully authenticated, but GitHub does not provide shell access.`说明已经成功

接下来克隆仓库到本地

进入github仓库右边code选择ssh点击右边复制

执行`git clone ssh地址`

这个时候就把仓库地址克隆到了本地

然后你可以测试push的时候还需不需要验证用户名和密码了

在仓库下创建test.cpp文件随便输入

a：`git add test.cpp`

b:	`git commit -m "注释内容"`

c:	`git push`

这个时候你会发现，不需要弹出用户名个密码就直接可以进行push了

## 解决http协议下每次push都需输入用户名密码

在本地仓库中找到config文件打开修改url

`用户名:密码@`

```c++
url = https://用户名:密码@github.com/pingfan443/git_test.git
```

# 分支管理

```c++
1;查看分支
    git branch
    注意:当前分治前面有个"*"标记。
2：创建分支
     git branch 分支名
3：切换分支
      git checkout dev  
4:合并分支
    git merge 被合并的分支名
    例如在dev分支下，写了一些东西，但是当你切换到master分支下，会发现没有写的东西，这个时候在master下执行git merge dev即可合并你写的东西
 5：删除分支
    git branch -d 分支名
    注意：删除分支之前一定要退出该分支
```
