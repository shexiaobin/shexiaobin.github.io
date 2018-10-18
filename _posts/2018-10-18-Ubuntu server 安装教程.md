---
layout:     post   				        # 使用的布局（不需要改）
title:      Ubuntu server 安装教程 		   # 标题 
subtitle:   Hello friend                #副标题
date:       2018-10-18				    # 时间
author:     shexiaobin 				    # 作者
header-img:  img/post-bg-2015.jpg     	#这篇文章标题背景图片
catalog: true 						    # 是否归档
tags:								    #标签
    - Linux
---


本意是想写Ubuntu 15.04 Server amd64系统的安装过程的，不过在找下载链接的时候看到了16.04的版本，忍不住想尝试一下，所以这里干脆换成Ubuntu 16.04 Server (64-bit)系统的安装吧，连标题也同步更换，不过装完之后才发现16.04的安装跟15.04的安装并无区别。不过需要说明的是：Ubuntu 15.04 Server (64-bit)系统的U盘启动工具的制作就跟Windows系统以及Linux各版本的desktop版不同，用的工具也是我第一次见到的“Win32_Disk_Imager”(下载见 [http://www.linuxidc.com/Linux/2013-10/91182.htm](https://www.linuxidc.com/Linux/2013-10/91182.htm) )。而Ubuntu 16.04 Server (64-bit)系统的U盘启动工具的制作可以直接使用软碟通，下载见 [http://www.linuxidc.com/Linux/2012-11/74577.htm](https://www.linuxidc.com/Linux/2012-11/74577.htm)。

实体机和虚拟机在Ubuntu 16.04 Server系统安装的过程中的步骤没有太大差别。

## 安装步骤

*   [下载系统镜像](http://www.ubuntu.com/download/alternative-downloads)或者直接[点击下载Ubuntu 16.04 Server (64-bit)](http://releases.ubuntu.com/16.04/)；

*   参照“[Hyper-V创建虚拟机](https://www.linuxidc.com/Linux/2016-04/129750.htm)”来创建虚拟机；[http://www.linuxidc.com/Linux/2016-04/129750.htm](https://www.linuxidc.com/Linux/2016-04/129750.htm)
    **注意**：在安装选项这一步，选择的操作系统为我们已经下载好的“Ubuntu 16.04 Server (64-bit)”镜像。

![image](http://upload-images.jianshu.io/upload_images/12269087-3fae8faf427eebe4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/12269087-6a63848c3f2eb9e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后“下一步”-“完成”。到此为止，我们已经创建好了虚拟机。接下启动并连接虚拟机。

![image](http://upload-images.jianshu.io/upload_images/12269087-b439f0dc70576936.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来，我们会进入系统安装的第一个界面，开始系统的安装操作。每一步的操作，左下角都会提示操作方式！！

1.选择系统语言-English；

![image](http://upload-images.jianshu.io/upload_images/12269087-23344a1dced970b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.选择操作-Install Ubuntu Server；

![image](http://upload-images.jianshu.io/upload_images/12269087-9a25f6490d5a225c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.选择安装过程和系统的默认语言-English；

![image](http://upload-images.jianshu.io/upload_images/12269087-785e1037b7141b99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.选择区域-other；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-665c32ed344786e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.选择亚洲-Asia；

![5.选择亚洲-Asia；](http://upload-images.jianshu.io/upload_images/12269087-15a17d1364aa7810.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.选择国家-China；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-0d5d78b2a4d2aba0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7.选择字符集编码-United States；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-900dc2690cf8b175.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.是否扫描和配置键盘，选择否-No；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-135f492d0f09cdd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9.选择键盘类型-English (US)；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-23f31196a51a440a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10.选择键盘布局-English (US)；

 ![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-fb9bac5ae5554980.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**更多详情见请继续阅读下一页的精彩内容**： [http://www.linuxidc.com/Linux/2017-11/148341p2.htm](https://www.linuxidc.com/Linux/2017-11/148341p2.htm)

11.设置主机名称(自行设置，这里我设置为“Docker06”)-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-b50b0e35b08efc8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

12.设置用户全名(这里为“Mongo”)-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-8ba5442dadfaf329.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

13.设置登录账号(这里为“mongo”)-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-93918c00e5356045.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

14.设置登录密码(空格选择“Show Password in Clear”可以显示密码)-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-c575588b8154b0f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-c50d354f467d4364.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

15.重复上一步设置的登录密码-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-50a0d6ad942bfdac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

16.是否加密home文件夹，选择否-No；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-4c80a236c5445d36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

17.确认时区是否正确(这里是“Asia/Shanghai”正确)，选择是-Yes；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-91dfd43eaa79ad97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

18.选择分区方式(分区向导-使用整个磁盘)-“Guided - use entire disk”；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-d1905e1a22a5d77e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

19.选择要分区的磁盘(这里只有一块)-“SCSI3 ···”；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-651812fa58f11044.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

20.是否将变更写入磁盘，选择是-Yes；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-15566bd90194df1d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

21.设置HTTP代理，无需填写直接下一步-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-e479729413b98a73.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

22.设置系统升级方式，选择自动升级-Install security updates automatically；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-ee36d9fcef2b4e54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

23.选择要安装的软件，多加一个OpenSSH Server，然后下一步-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-097f9d5ef5bc9701.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

24.是否安装GRUB引导程序，选择是-Yes；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-5b8121d4df94373f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

25.完成安装，选择下一步-Continue；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-d3dcbfd682883629.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

26.系统安装完会自动启动主机，然后输入设置好的登录账户和密码就可以开始使用了；

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-c132137de285c5cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Ubuntu 16.04 Server 版安装过程图文详解](http://upload-images.jianshu.io/upload_images/12269087-74c59040c581904b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

来源:https://m.linuxidc.com/Linux/2017-11/148341.htm
