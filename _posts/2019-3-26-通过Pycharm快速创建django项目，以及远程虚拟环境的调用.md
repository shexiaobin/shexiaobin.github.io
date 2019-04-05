---
layout:     post   				        # 使用的布局（不需要改）
title:      通过Pycharm快速创建django项目，以及远程虚拟环境的调用	   # 标题 
subtitle:   同步项目                #副标题
date:       2019-03-26				    # 时间
author:     Mayer					    # 作者
header-img:  img/post-bg-YesOrNo.jpg       	#这篇文章标题背景图片
catalog: true 						    # 是否归档
tags:								    #标签
    - Python
---



# 关于Django
**Django 是一个用 Python 语言写的开源 Web 框架，可帮助开发人员在构想形成后仅数小时内启动 Web 应用程序。它遵循模型视图模板 (MVT) 来构建应用程序，这可降低 Web 开发的复杂性，同时可让开发人员集中精力编写应用程序。它为网站地图、内容管理、用户鉴权、RSS 提要及其他任务提供开箱即用的设置。一些高流量网站使用 Django 是因为它能够快速、灵活地进行调整，从而可满足流量波动高峰期的需求。**

# 在Pycharm上创建项目

![image.png](https://upload-images.jianshu.io/upload_images/12269087-2ff4760fd1fe7b08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



![image.png](https://upload-images.jianshu.io/upload_images/12269087-d630c5ef92f8a3d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 连接服务器

![image.png](https://upload-images.jianshu.io/upload_images/12269087-9e68a8da5b5823ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/12269087-1f20663496427a57.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 选择环境 
![image.png](https://upload-images.jianshu.io/upload_images/12269087-fdbd14e3e758d3a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 创建成功
![image.png](https://upload-images.jianshu.io/upload_images/12269087-d7c6ac6bde1c54f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 运行Django项目

  * 在PyCharm中，修改`setting.py`
将settings.py文件中的


```ALLOWED_HOSTS = [ ],改成ALLOWED_HOSTS = ['*']```


或者



```
ALLOWED_HOSTS = [
    '.example.com',  # Allow domain and subdomains
    '.example.com.',  # Also allow FQDN and subdomains
    '139.198.xxx.xxx', # 测试环境我们一般允许自己的主机IP访问即可
]
```

## 开启服务有两种方式：
* 在Ubuntu16.04下开启服务，运行下面的命令（~/djtest11是项目目录）：
```
$ cd ~/djtest11
$ python manage.py runserver 0.0.0.0:8000
```
![image.png](https://upload-images.jianshu.io/upload_images/12269087-c3652d2866951735.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*  在PyCharm中开启服务

       选择编辑器右上角的【Add Configuration】的按钮

![image.png](https://upload-images.jianshu.io/upload_images/12269087-10ff1b498b2a2d41.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


  点击【+】
     
         
![image.png](https://upload-images.jianshu.io/upload_images/12269087-3bea7a5f754cb1f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


    点击添加【Django server 】

![image.png](https://upload-images.jianshu.io/upload_images/12269087-8c81873b529d9707.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


    设置Name、修改Host为0.0.0.0，表示的是服务在哪个IP监听


![image.png](https://upload-images.jianshu.io/upload_images/12269087-8e2548f271d44d13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


      点击【Fix】，在弹出窗口，选中【Django】,
      在右侧选择本地项目目录，选择Settings文件路径。
      
      

![image.png](https://upload-images.jianshu.io/upload_images/12269087-cb4762fe8d25675d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


（说明，如果看不到【Fix】按钮，在【Environment variables】中添加名为“DJANGO_SETTINGS_MODULE”，值为“项目名.settings”的环境变量）


![image.png](https://upload-images.jianshu.io/upload_images/12269087-c72e58be2d086b43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


点击绿色三角形，启动服务

![image.png](https://upload-images.jianshu.io/upload_images/12269087-911510c92f5a7d48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# 使用Pycharm同步项目

## 创建django工程

在Ubuntu 16.04下执行下面的命令。
（1）创建一个python3的虚拟环境（如果已经创建，忽略此步）
```$ conda create --name py3 python=3```

（2）进入该虚拟环境
```$ conda activate py3```

（3）安装django
```$ conda install django```

（4）新建项目
 (注意: 由于编辑器版本之间的一些差别, 我们统一使用跟编辑器版本无关的通用方式创建项目。先在命令行创建项目，然后再设置PyCharm代码同步)
采用以下命令创建项目，projectname表示项目名可修改。

![image.png](https://upload-images.jianshu.io/upload_images/12269087-c2de98473be3379a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用tree命令查看目录结构，如果没有tree命令，则先安装。

```
$ sudo apt-get install tree
$ cd djtest11
$ tree
```
各文件作用如下：

![image.png](https://upload-images.jianshu.io/upload_images/12269087-cfbf7a0bb8a8476e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 同步

* 用PyCharm创建一个项目

![image.png](https://upload-images.jianshu.io/upload_images/12269087-6d1dc83497b2c126.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 解释器选择上面创建的虚拟环境中的python3.7，本示例中，解释器的路径为：
`/home/hadoop/anaconda3/envs/py3/bin/python3.7`

![image.png](https://upload-images.jianshu.io/upload_images/12269087-c00d4e3f2ffb535b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 远端项目的路径选择上面创建的项目路径（注意不要选择内层同名的目录）。

![image.png](https://upload-images.jianshu.io/upload_images/12269087-57a23e4e0dbfe6b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


点【确定】后效果如下：

![image.png](https://upload-images.jianshu.io/upload_images/12269087-b0042ff6fe792f02.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点【Create】后完成创建。


* 选择【Tools】-【Deployment】-【Download ...】下载项目文件到本地。

**在此之前，记住要选择py_001,不然你会发现无法Download**

![image.png](https://upload-images.jianshu.io/upload_images/12269087-ae0a71c03154be96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/12269087-6575f75e0cb13a17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 同步后的项目代码如下：

![image.png](https://upload-images.jianshu.io/upload_images/12269087-8282601104df5dd2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# 常用命令总结

 ```

django-admin startproject projectname    #新建项目命令

python manange.py startapp app_name   #创建命令

python manage.py runserver 0.0.0.0:8000    #改动文件后，都需要runserver一下

```
# windows上创建第一个django项目

[在windows上创建第一个django项目参考链接](https://www.django.cn/article/show-7.html)

注意一点不同：图片位置最好选上


![image.png](https://upload-images.jianshu.io/upload_images/12269087-0bdde89ce4f30031.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# [PyCharm如何创建新工程以及连接Linux环境(https://www.jianshu.com/p/a1fc4b71eb9b)
