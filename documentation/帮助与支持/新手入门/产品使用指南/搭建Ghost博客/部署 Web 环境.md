本节介绍如何部署 Web 环境，以安装 Nginx为例：

软件包中包含的软件及版本如下：

* nginx：1.10.2

说明：这是写文档时参考的软件版本。您下载的版本可能与此不同。

### []()[]()

* 确保您安装了连接 Linux 实例的工具，如 xshell。
* 打开 xshell ，设置登录实例所需的信息。
* 设置连接名称。
* 协议选择 SSH。
* 输入主机 IP 地址和用户名

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-17.png)

* 输入用户名 root 和登录密码。

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-18.png)

* 添加Nginx软件库：

[root@softwaretest ~]/# rpm -Uvh [http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm](http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm)

* 安装Nginx：

[root@softwaretest ~]/# yum -y install nginx

* 设置Nginx服务器自动启动：

[root@softwaretest ~]/# systemctl enable nginx.service

* 启动Nginx并查看Nginx服务状态：

[root@softwaretest ~]/# systemctl start nginx.service

[root@softwaretest ~]/# systemctl status nginx.service

* 在浏览器中输入公网IP地址，可以看到默认的Nginx的网页
![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-19.png)

至此，Nginx搭建完成