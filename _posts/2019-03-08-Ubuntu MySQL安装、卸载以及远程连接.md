---
layout:     post   				        # 使用的布局（不需要改）
title:      Ubuntu MySQL安装、卸载以及远程连接 		   # 标题 
subtitle:   mysql卸载安装             #副标题
date:       2020-03-08 				    # 时间
author:     shexiaobin 				    # 作者
header-img:  img/post-bg-digital-native.jpg     	#这篇文章标题背景图片
catalog: true 						    # 是否归档
tags:								    #标签
    - SQL
---




# Ubuntu MySQL安装、卸载以及远程连接

# 1. 安装😃

- ### 查看apt list中MySQL版本信息

```mysql
apt list | grep mysql-server
```

![image](https://user-images.githubusercontent.com/26622879/69494767-5fcb6700-0efa-11ea-917e-21ccdfa63f76.png)

- 安装mysql

```mysql
# 会提示让你输入密码（两次）
sudo apt-get install -y mysql-server
```

- 操作MySQL服务

```mysql
#启动
sudo service mysql start 
#停止
sudo service mysql stop
#重启
sudo service mysql restart
```

# 2. 卸载



- `` dpkg --list|grep mysql `` 查看自己的mysql有哪些依赖 

![image](https://user-images.githubusercontent.com/26622879/69494809-f5ff8d00-0efa-11ea-8491-fd1b2c071671.png)

```shell
# 逐个卸载
sudo apt-get remove mysql-common
sudo apt-get autoremove --purge mysql-server-5.7
#再用dpkg --list|grep mysql查看，还剩什么就卸载什么

#最后清楚残留数据：
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

> 一定要卸载干净，不然重新安装会不成功

# 3. 远程连接

```mysql
# 登录MySQL
mysql -uroot -p
show databases;
use mysql；
select host from user where user='root';
# Host设置为通配符%。
update user set host = '%' where user ='root';
```

- 修改配置文件

```mysql
sudo /etc/mysql/mysql.conf.d/mysqld.cnf
# 将bind_address=127.0.0.1注释掉.
# 并添加一行  
bind_address=0.0.0.0
# 然后重启服务
/etc/init.d/mysql restart
```

![image](https://user-images.githubusercontent.com/26622879/69494928-1c71f800-0efc-11ea-80ab-63fee2b3df97.png)

- ### 修改配置文件设置数据写入格式utf-8

```shell
#打开配置文件
vi /et/mysql/my.cnf
```

​		将下面的加入配置

```mysql
[client]
default_character_set=utf8 
[mysql]
default_character_set=utf8 
[mysqld]
character_set_server=utf8
```

>  重启mysql，重启mysql，重启mysql

- 确保防火墙允许 3306 端口开启

```mysql
1. 开启防火墙 【PS：某些情况下 Ubuntu 可能默认的防火墙没有开启，这样的话就不用关心防火墙造成的影响，但是云服务器在生产环境下，我们为了安全通常是开启防火墙的，这时候我们需要知晓该如何配置】
`sudo ufw enable/disable` # 开启或者关闭防火墙 
# 更多操作大家可以使用 ufw --help 查看

# 添加允许规则
> sudo ufw allow 3306/tcp 
# 查看已添加规则
sudo ufw status

# debian 系列的防火墙软件为 ufw, Ubuntu 是基于 debian 的，Centos 属于红帽系列，防火墙软件不是 ufw,具体可以自行搜素哦
```

# 4. 无法登录：'root'@'localhost'

 ubuntu下，ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: yes)的解决方案

1.命令行输入：``sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf``

> 在[mysqld]后面任意一行添加 “skip-grant-tables” 用来跳过密码验证的过程
>
> 保存文档并退出 :wq

2.接下来我们需要重启MySQL：/etc/init.d/mysql restart

显示如下：

```mysql
[....] Restarting mysql (via systemctl): mysql.serviceFailed to add /run/systemd/ask-password to directory watch: No space left on device
. ok 
```

3.重启之后输入  #mysql 即可进入mysql。

4.接下来就是用sql来修改root的密码

```mysql
mysql> use mysql;
mysql>update mysql.user set authentication_string=password('123456') where user='root';
mysql> flush privileges;
mysql> quit
# 此时root账户就已经重置成新的密码了。
```

```mysql
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
# 编辑mysqld.cnf,去掉刚才添加的内容，然后重启MySQL, 
/etc/init.d/mysql restart 大功告成！
```



