**Ubuntu环境下通过Apt-get安装**

为了提升用户在云服务器上的软件安装效率，减少下载和安装软件的成本，京东云提供了Apt-get下载源。操作系统为Ubuntu12.04的云服务器，用户可通过Apt-get快速安装软件。京东云会在每天02:00-04:00从archive.Ubuntu.com对下载源进行同步。

在下载软件之前，您需要进行相关配置：

对于Ubuntu系统：

1. 
备份
mv /etc/apt/sources.list /etc/apt/sources.list.backup
1. 
vi /etc/apt/sources.list
1. 
新增源

Ubuntu 12.04

debhttp://mirrors.jcloudcs.com/ubuntu/precise main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/precise-security main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/precise-updates main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/precise-proposed main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/precise-backports main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/precise main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/precise-security main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/precise-updates main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/precise-proposed main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/precise-backports main restricted universe multiverse

Ubuntu 14.04

deb [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.jcloudcs.com/ubuntu/) trusty main restricted universe multiverse

deb [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-security main restricted universe multiverse

deb [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-updates main restricted universe multiverse

deb [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-proposed main restricted universe multiverse

deb [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-backports main restricted universe multiverse

deb-src [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty main restricted universe multiverse

deb-src [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-security main restricted universe multiverse

deb-src [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-updates main restricted universe multiverse

deb-src [http://mirrors.jcloudcs.com/ubuntu/](http://mirrors.aliyun.com/ubuntu/) trusty-proposed main restricted universe multiverse

Ubuntu 16.04

debhttp://mirrors.jcloudcs.com/ubuntu/trusty main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty-backports main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/trusty-security main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/trusty-updates main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/trusty-proposed main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/trusty-backports main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty-security main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty-updates main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty-proposed main restricted universe multiverse

deb-srchttp://mirrors.jcloudcs.com/ubuntu/trusty-backports main restricted universe multiverse

debhttp://mirrors.jcloudcs.com/ubuntu/xenial main restricted

deb-srchttp://mirrors.jcloudcs.com/ubuntu/xenial main restricted

debhttp://mirrors.jcloudcs.com/ubuntu/xenial-updates main restricted

deb-srchttp://mirrors.jcloudcs.com/ubuntu/xenial-updates main restricted

debhttp://mirrors.jcloudcs.com/ubuntu/xenial universe

deb-srchttp://mirrors.jcloudcs.com/ubuntu/xenial universe

debhttp://mirrors.jcloudcs.com/ubuntu/xenial-updates universe

deb-srchttp://mirrors.jcloudcs.com/ubuntu/xenial-updates universe

4. 更新源 apt-get update

配置完成后即可根据需要下载安装软件。

## **1. 安装步骤**

1) 登录操作系统为Ubuntu12.04的云服务器

2) 通过以下命令安装软件：

sudo apt-get install

示例如下：

sudo apt-get install nginx php5-cli php5-cgi php5-fpm php5-mcrypt php5-mysql mysql-client-core-5.5 mysql-server-core-5.5

结果：

![](https://img1.jcloudcs.com/cms/04dcb4a1-4130-4e20-a8e2-5cfe1b1d685c20170330190732.png)

3) 输入“Y”确认后，开始安装软件，直至软件安装完成。

## **2. 查看安装的软件信息**

软件安装完成后，可通过以下命令查看软件包所在的目录，及该软件包中的所有文件：

sudo dpkg -L

可通过以下命令查看软件包的版本信息：

sudo dpkg -l

示例如下：

sudo dpkg -L nginx sudo dpkg -l nginx

结果如下（实际的版本可能和此版本不一致，请以实际查询到的版本为准）：

![](https://img1.jcloudcs.com/cms/73b4fa0c-812d-444a-b809-4fb036fa9e9b20170330190810.png)![](https://img1.jcloudcs.com/cms/4c58127c-2b26-44cf-9124-1a63d9f8e15820170330190813.png)