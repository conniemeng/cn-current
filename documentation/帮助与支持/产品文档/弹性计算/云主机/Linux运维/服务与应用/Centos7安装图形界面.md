**Centos7安装图形界面**

登录云主机，执行命令：

1.yum -y groupinstall "X Window System" /#安装x window包 2.yum -y groupinstall "GNOME Desktop" /#安装Gnome包 3.ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target /#运行级别启动图形界面 4.reboot /#重启服务器生效

重启后通过云主机控制台，远程连接vnc功能登录，可以看到图形界面，如图：

![1.png](https://img1.jcloudcs.com/cms/d9a71ed2-8434-4b62-9bd6-0310412a34c920171222160934.png)

如无法解决您的问题，请向我们提工单。