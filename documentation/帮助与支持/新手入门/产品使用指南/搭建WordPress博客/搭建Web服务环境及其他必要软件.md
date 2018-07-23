在云主机中安装必要的支持软件，包括Nginx，PHP运行环境，PHP MySQL扩展。

**1.更新yum源：**/#yum update；

**2.安装nginx ：**/#yum install nginx；

**3.****启动nginx:**/#systemctl start nginx.service

**4.本地浏览器中输入公网IP，出现如下页面，则nginx安装成功**

![](https://img1.jcloudcs.com/cms/57c6db14-0404-4d52-bbe6-3d5cc9d0501120170313153217.png)

**5. 安装PHP执行环境**

需安装php以及php-fpm，使用CentOS 7.3镜像自带的yum源即可。

1）安装php：/#yum install php

2）安装php-fpm：/# yum install -y php-fpm

3) 启动php-fpm: /# systemctl start php-fpm.service

**6.安装 php-mysql:**

/# yum install -y php-mysql