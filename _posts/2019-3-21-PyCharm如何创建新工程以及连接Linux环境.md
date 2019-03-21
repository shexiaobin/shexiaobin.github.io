---
layout:     post   				        # 使用的布局（不需要改）
title:      PyCharm如何创建新工程以及连接Linux环境	   # 标题 
subtitle:   Hello friend                #副标题
date:       2019-03-21				    # 时间
author:     Mayer					    # 作者
header-img:  img/post-bg-YesOrNo.jpg       	#这篇文章标题背景图片
catalog: true 						    # 是否归档
tags:								    #标签
    - Python
---





	* 准备工作：阿里云（Ubuntu16.0.4）
		       PyCharm专业版


![Snipaste_2019-03-21_14-25-55.png](https://upload-images.jianshu.io/upload_images/12269087-24f83310d9ac8a8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 设置本地路径
![image.png](https://upload-images.jianshu.io/upload_images/12269087-e3cea2002c4f4e91.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	
## 设置虚拟机Python解释器环境

![image.png](https://upload-images.jianshu.io/upload_images/12269087-d99613493d0b3986.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	* ssh连接虚拟机

![image.png](https://upload-images.jianshu.io/upload_images/12269087-ffcdcb4b7abfb26f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	*next后，输入密码

![image.png](https://upload-images.jianshu.io/upload_images/12269087-68bc7408f87f6963.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


	* 选择Linux上的python环境，我们这里选择py3.7
	* 注意查看路径 /home/shexiaobin/anaconda3/bin/python3.7

![image.png](https://upload-images.jianshu.io/upload_images/12269087-4c3e27d764b15201.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


	*设置代码上传路径

![image.png](https://upload-images.jianshu.io/upload_images/12269087-f49db9b2d51da4d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 测试

	在PyCharm中新建python file


```
print('hello')
```
	 
	查看Linux上对应的目录是否有文件生成

```
python xxx.py
```
## 注意

	下次创建项目时，用第一次创建的解析器环境即可