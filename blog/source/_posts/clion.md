---
title: clion解决多个源文件编译
date: 2020-07-02 11:21:24
tags: clion解决多个源文件编译
category: clion
index_img: https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702154533.png
---


# Clion如何编译运行多个源文件？

##  **1新建工程编译运行单个源文件**
<!-- ![clion--1.png](https://i.loli.net/2020/07/02/FPhDUubKpsL8k92.png) -->
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152655.png)
 

## **2运行第二个源文件**

**此时你会发现报错！！！**
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152253.png)
<!-- ![clion-2 _1_.png](https://i.loli.net/2020/07/02/CHUaE5vh3yqApul.png) -->

# **解决办法1：**

 

**修改cmakelist.text，将**

add_executable(prc1 main.cpp )改成

add_executable(prc1 practice/test1.cpp )就行了

 
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152658.png)
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152657.png)
<!-- ![clion-3 _1_.png](https://i.loli.net/2020/07/02/UT2wROhCn7DuHXF.png) -->

<!-- ![clion-4 _1_.png](https://i.loli.net/2020/07/02/oe5wc8pZEUjgBPi.png) -->

 

## **效果如下**



<!-- ![clion-5 _1_.png](https://i.loli.net/2020/07/02/2khBLw1jDtrNx79.png) -->
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152700.png)
 

**但是这样是不是好费劲？每次都要修改cmakelist.text，尤其是对于那些刷题的同学，=~=！接下来给大家提供一个插件解决这个复杂的问题**

 

# 解决办法2：下载插件

**左上角file下点击setting进入**

 
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152659.png)
<!-- ![clion-6 _1_.png](https://i.loli.net/2020/07/02/ZVWuvarPhcECeTL.png) -->



**下载之后我们创建一个源文件，进行测试**

**在test2下右击鼠标，点击箭头**
<!-- ![clion-7 _1_.png](https://i.loli.net/2020/07/02/zCBfgEYnWAPMSDm.png) -->
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152656.png)
**自动为我们添加add_executable(test2 practice/test2.cpp)**
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152701.png)
<!-- ![clion-8 _1_.png](https://i.loli.net/2020/07/02/OAGFYD5EtqHh79K.png) -->

 

**最后你就可以直接run了（run之前记得切换到你的源文件下！！！！重点）**
![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs20200702152702.png)
<!-- ![clion-9 _1_.png](https://i.loli.net/2020/07/02/jnP12kMOQJS3NsY.png) -->

 

 