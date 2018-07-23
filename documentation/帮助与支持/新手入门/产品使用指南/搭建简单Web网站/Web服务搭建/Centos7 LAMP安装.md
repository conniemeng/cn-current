# **Centos7 LAMP安装**

## **LAMP简介：**

LAMP是指一组通常一起使用来运行动态网站或者服务器的自由软件名称首字母缩写：

* 
Linux，操作系统
* 
Apache，网页服务器
* 
MariaDB或MySQL，数据库管理系统（或者数据库服务器）
* 
PHP、Perl或Python，脚本语言

虽然这些开放源代码程序本身并不是专门设计成同另几个程序一起工作的，但由于它们的廉价和普遍，这个组合开始流行（大多数Linux发行版本捆绑了这些软件）。当一起使用的时候，它们表现的像一个具有活力的“解决方案包”（Solution Packages）。

## **测试环境说明**

OS：CentOS Linux release 7.1.1503 (Core)

Kernel：3.10.0-229.20.1.el7.x86_64

## **操作流程说明**

1. 
初始化安装环境
1. 
进行Apache的安装
1. 
验证Apache是否安装成功
1. 
安装php
1. 
验证php是否安装成功
1. 
安装MariaDB数据库
1. 
使用PHPAdmin管理MariaDB数据库（应用）

## **具体步骤**

### **初始化安装环境**

安装开始之前，需要进行安装环境的初始化，开启安装EPEL YUM源。这是因为CentOS默认只使用官方的YUM，里面大约有4000多个RPM包，但是EPEL源中的包则有10000多个，极大的方便了我们安装第三方软件：

/#yum –y epel-release

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-734.png)

使用下面的命令来显示本地启动的YUM仓库

/#yum repolist

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-735.png)

### **安装Apache服务**

### 使用yum方式来安装Apache程序

在CentOS中，Apache作为常用软件包在官方的yum源中就可以找到，使用下面的命令来完成Apache的安装

/#yum –y install httpd

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-736.png)

如图Yum会自动完成依赖关系的解决，实现Apach的安装

### **启动Apache服务**

安装成功之后，可以使用下面的命令来管理Apche程序

/#systemctl enable httpd //设置开机启动httpd程序

/#systemc start httpd //启动httpd服务

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-737.png)

完成上述两条命令之后便可以启动httpd服务了。您可以使用下面的这一条命令来查看httpd服务的运行状态：

/#systemctl status httpd

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-738.png)

### **验证Apache服务**

### 查看您的端口监听状态：

使用下面的命令可以查看当前主机监听tcp端口：

/#netstat –tnl

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-739.png)

### **查看您的防火墙配置：**

CentOS 7上提供了firewall工具来帮助我们管理防火墙，使用下面的命令可以禁止防火墙运行：

/#systemctl stop firewalld

但是在生产环境中，您最好使您的防火墙处于开启状态并只开启必要端口保证主机不被入侵。下面的命令用来启动您本机的防火墙

/#systemctl enable firewalld

/#systemctl start firewalld

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-740.png)

### **防火墙允许http流量通过**

如果您选择关闭防火墙，这个过程是不必要执行的

使用如下的命令来是firewall永久放行http流量

/#firewall-cmd –permanent –add-service=http

在此命令运行之后，为了使配置生效需要使firewall重读配置文件

/#firewall-cmd –reload

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-741.png)

您可以使用下面的命令来检查防火墙当前所有的规则：

/#firewall-cmd –list-all

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-742.png)

### **验证Apache初始网页**

您可以在浏览器中输入您主机的公网地址来查看相应的网页

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-101.jpeg)

至此，Apache就安装成功了。

### **安装PHP**

PHP是一种通用开源脚本语言。语法吸收了C语言、Java和Perl的特点，利于学习，使用广泛，主要适用于Web开发领域。PHP 独特的语法混合了C、Java、Perl以及PHP自创的语法。它可以比CGI或者Perl更快速地执行动态网页。配合Apache来实现对外提供动态网页服务

这里安装PHP主要是为了一些动态网页来提供运行环境，PHP的安装包同样存在于官方的YUM源中，使用以下的命令可以来安装PHP及其相关组件

/#yum –y install php php-mysql

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-743.png)

默认安装PHP5.4版本，至此PHP安装结束

### **验证PHP运行**

通过运行PHP代码可以验证我们的PHP环境是否正确安装。

### 生成PHP测试文件：

/#echo -e “<?php\nphpinfo();\n?>” > /var/www/html/test.php

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-744.png)

通过运行上述命令，在Apache默认网页根目录中生成test.php文件。

### **重启httpd服务**

由于安装了PHP，Apache的运行配置发生了改变需要重新读取配置文件，在验证之前先重启一下httpd程序：

/#systemctl restart httpd

### **验证PHP环境：**

通过在浏览器中输入下面的地址来访问PHP测试网页

http：//主机公网IP/test.php

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-102.jpeg)

可以验证PHP正确安装。

### **安装配置MariaDB数据库**

MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可 MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。在存储引擎方面，使用XtraDB（英语：XtraDB）来代替MySQL的InnoDB。

### **安装MariaDB数据库**

和Apache，PHP一样，MariaDB同样在CentOS官方YUM中就有提供，使用以下命令安装MariaDB的相关组件

/#yum –y install mariadb mariadb-server

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-745.png)

等待安装完成之后，接下来就是启动数据库了，使用与启动Apache类似的命令

/#systemctl enable mariadb

/#systemctl start mariadb

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-746.png)

当然，使用下面的命令能够查看MariaDB的运行状态

/#systemctl status mariadb

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-747.png)

### **运行数据库初始化脚本**

为了方便我们使用数据库，MariaDB提供了一个初始化脚本来帮助我们快速使用

/#mysql_secure_installation

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-103.jpeg)

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-104.jpeg)

### **登录数据库进行验证**

使用下面的命令即可以root身份对数据库进行管理

/#mysql –u root –p

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-748.png)

如图所示，输入密码之后便可以进入到数据库的管理界面

## **应用**

完成上述的LAMP环境搭建后，我们就可以使用这个PHPAdmin工具在Web界面中管理MairaDB数据库了，下面是具体的操作方法

### **环境初始化：**

虽然通过上述操作已经安装过PHP环境了，但是想要操作数据库，还要安装以下的这些php组件：

/# yum -y install php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-soap curl curl-devel

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-749.png)

安装完成之后重启一下httpd程序：

/#systemctl restart httpd

### **安装PHPMyAdmin工具**

由于我们已经同步过EPEL源，直接使用下面的命令安装即可

/#yum –y install phpmyadmin

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-750.png)

等待安装完成即可

### **配置PHPMyAdmin**

由于PHPMyAdmin默认只允许本地来通过网页管理数据库，所以如果我们想要远程使用PHPAdmin就需要修改其配置文件：

/# vim /etc/httpd/conf.d/phpMyAdmin.conf

注：如果命令运行失败，先运行命令/#yum –y install vim安装vim编辑器

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-751.png)

通过方向键来移动光标，按“i”键进入编辑模式，修改如下内容

在Require ip 127.0.0.1，Require ::1之前添加/#

添加：Require all granted

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-752.png)

编辑完成之后按“Esc”键退出编辑模式，输入“:wq”保存退出

修改完配置之后重启httpd程序：

/#systemctl restart httpd

### **通过浏览器访问PHPMyAdmin来验证**

通过输入以下内容访问PHPMyAdmin

/#http://主机公网IP/phpmyadmin

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-105.jpeg)

输入用户名root，和您之前设置的密码就可以访问管理界面了

![](http://cloudway.jcloud.com/wp-content/uploads/2017/06/word-image-106.jpeg)