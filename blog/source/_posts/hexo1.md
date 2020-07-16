---
title: hexo学习系列（一）
date: 2020-07-15 18:36:28
tags: hexo搭建博客
category: hexo
index_img: https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs/20200715184608.png
---

# 搭建博客的准备工作

1. 下载node.js
2. 下载git

安装直接一路就行了，最好找个教程看看，因为其中有一步选的不合试，还得自己配置环境变量，也有选项直接是帮你配置好的。看自己情况即可

```c++
git安装教程：https://blog.csdn.net/sanxd/article/details/82624127?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase
如果发现git在cmd中输入git找不到命令是因为没有配置环境变量，需要自己配置环境静变量（附带教程：https://www.cnblogs.com/-mrl/p/11246666.html）另外这个其实也不需要一定要配置，也可以直接在git bash中直接运行即可。
```

# hexo搭建博客

以上两个应用安装后，通过以下命令来测试：
`node -v`		测试node版本，有版本信息即说明安装成功
`git version`	测试git版本，同上
以上两步，如果是找不到命令，一般情况就是配置环境变量有问题或者说没有配置环境变量

先在某盘(这里是E盘)下创建个文件夹Project

**注意**：以下命令在cmd中执行，当创建完blog文件夹时，所有命令都是在blog目录下执行

两种方式搭建hexo

1. 在project下创建一个blog文件然后打开blog执行`hexo init`就会创建hexo
2. 在project下 执行 `hexo init blog` 同上述操作一样，但执行完后要cmd要在blog目录下去执行其他命令

**说明**：生成我们所需要的文件，这里可能会出错，err，然后我们可以进入到生成的文件，在运行 npm  install 把刚才没有装上的包再装一下，这里你会发现blog下有8个文件，如果没有，说明少安装了，可以通过npm cache clean --force  清理一下缓存在使用npm install 命令安装 成功安装了8个文件

## 安装hexo

以下命令在cmd中执行，并且是在E:\Project\blog下

1. `npm install -g hexo-cli`

安装hexo（cli就是命令行，接口，这里如果安装缓慢可以使用淘宝镜像源

`npm config set registry https://registry.npm.taobao.org`，然后在执行该命令）

2. `hexo g `

生成网站页面（此时会发现blog文件夹下多了个public文件，这个就是网页文件）

3. `hexo s`

s就是serve的意思，复制网址到浏览器即可在本地查看到一个静态网页  

## hexo常用命令

1. `hexo new "post title"`

说明：hexo new 命令默认是生成博客文章，但是同样也可以生成草稿以及纯文件，生成的文章在source/_posts下

引号里边是文章标题
然后通过vscode打开blog文件，找到source下的上边你写的那个标题"post title"可以在里边用markdown格式写一些东西，例如：(会md语法即可)

```c++
# 标题一
## 标题二
### 标题3
*这是斜体*
--这是横线--
1. 有序列表
> 引用
```

[vscode安装教程附带python安装环境](https://www.bilibili.com/video/BV1W7411T7NZ)

## 

