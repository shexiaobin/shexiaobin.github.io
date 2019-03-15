---
layout:     post   				        # 使用的布局（不需要改）
title:      Ubuntu虚拟机如何设置固定ip	   # 标题 
subtitle:   Hello friend                #副标题
date:       2019-03-14				    # 时间
author:     Mayer					    # 作者
header-img:  img/post-bg-YesOrNo.jpg       	#这篇文章标题背景图片
catalog: true 						    # 是否归档
tags:								    #标签
    - Linux
---






# 前言

**最近自己搞了一个hadoop的完全分布，因为虚拟机采用的是NAT模式，饱受了隔一段时间ip就自动改变的苦恼。而且我在网络方面实在是小白一个，什么网关，子网ip之类的知识完全就是一白空白，也苦恼于网络上的教程太杂，踩了很多坑，所以决定自己写一个。**

**当前环境：**

**虚拟机版本:VMware WorkStation 12**

**系统版本:Ubuntu 16.04**



# 一、查看windows的ip和网关

- ``ipconfig``查看
- 记住ip地址

![image.png](https://upload-images.jianshu.io/upload_images/12269087-2716b5ed44c4cd86.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 二、修改VMWare中的配置

## （1）修改子网ip

![image.png](https://upload-images.jianshu.io/upload_images/12269087-2f4d64c66d48cd78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## （2）查看NAT设置
   -  记住改网关ip

![image.png](C:\Users\Administrator\Documents\GitHub\shexiaobin.github.io\img\12269087-189fb4c8c9aa5e36.png)


# 三、修改interfaces文件 
``sudo vim /etc/network/interfaces``

![image.png](https://upload-images.jianshu.io/upload_images/12269087-6d1b6e104f15fb83.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
# The primary network interface
# iface ens33 inet dhcp

#开启自动启动网卡，输入ifconfig可以查看是否为ens33
auto ens33
#使用静态ip       
iface ens33 inet static
#设置IP，记住前面的192.168.1要和设置的子网ip保持一致
address 192.168.1.132
#子网掩码
netmask 255.255.255.0
#网关ip
gateway 192.168.1.2
#指定DNS服务器，可以使用我这个公共的DNS，这句一定要有
dns-nameserver 119.29.29.29

```


#  四、重启服务 
``sudo /etc/init.d/networking restart``
> 最好重启一下虚拟机

# 五、测试
## ``ping``

![image.png](https://upload-images.jianshu.io/upload_images/12269087-0329d227a66eebeb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/12269087-31ebac5b00b2c98e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
