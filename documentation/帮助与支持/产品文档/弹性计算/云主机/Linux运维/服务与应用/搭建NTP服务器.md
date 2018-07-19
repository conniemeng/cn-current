# **搭建NTP服务器**

以ubuntu 14.04为例，在同一子网内，一台云主机作为Server端通过公网IP同步时间，其余云主机作为Client端通过内网IP与Server端同步时间。

准备工作，该子网所在路由器绑定的防火墙规则必须允许端口 123 的入站UDP流量。

### **1.server端**

1）安装

命令：sudo apt-get install ntp

若无法安装先更新update源，命令：sudo apt-get update

2）配置

命令：sudo vim /etc/ntp.conf

配置内容及解析：
/# 时间源服务器 ，以官方提供的server举例，//www.pool.ntp.org/zone/cn
server 2.cn.pool.ntp.org
server 1.asia.pool.ntp.org server 0.asia.pool.ntp.org /# 连不上其他服务器时与LOCAL对时，使能够把本机时间给其他client提供服务
server 127.127.1.0 fudge 127.127.1.0 stratum 8 /# 还要确保localhost有足够权限. restrict 127.0.0.1 restrict ::1 /#client端所在的内部网段，以CIDR：192.168.5.0/28举例。nomodify：表示Client 端不能更改 Server 端的时间参数，不过Client端仍然可以透过Server 端來进行网络较时。 restrict 192.168.5.0 mask 255.255.255.240 nomodify

3）启动

命令：sudo /etc/init.d/ntp start

重启命令：sudo /etc/init.d/ntp restart

ntp 服务器上启动ntp服务后，ntp 服务器自身或者与其自身的同步需要一个时间段，这个过程可能是3-5分钟，在这个时间之内在客户端上运行sudo ntpdate server内网ip 命令时会产生no server suitable for synchronization found的错误。所以要等几分钟后再在客户端上执行同步时间的命令。

4）查看

命令：ntpq -4p

### **2.client端**

1）安装ntpdate

命令：sudo apt-get install ntpdate

2）同步server时间，以server内网ip为192.168.5.6举例，返回adjust time则您已完成整套操作。

命令：sudo ntpdate 192.168.5.6