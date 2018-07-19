**Centos安装配置vncserver**

本文中仅讨论VNC的安装，关于图形界面需要您另行安装。

****

**CentOS 6.5 安装 VNC Server**

**安装**

使用以下命令安装vncserver：

yum -y install tigervnc-server

![3.png](https://img1.jcloudcs.com/cms/e45ae7d6-c17f-472f-afc5-64fd1bd022e420170808160058.png)

**配置**

1.配置为开机自启动，使用以下命令将服务配置为开机自动启动：

chkconfig --level 345 vncserver on

![4.png](https://img1.jcloudcs.com/cms/21767b28-e4d7-4d3f-9c3d-2b641946ea4620170808160407.png)

2.配置置客户端连接密码，输入以下命令后进行 VNC 密码的设置：

vncserver

![6.png](https://img1.jcloudcs.com/cms/827bdadd-3a9d-4e58-88c9-5d0401ad0cdf20170808160248.png)

3.配置使用 GNOME 桌面，执行命令vi/root/.vnc/xstartup修改文件，把最后的 twm & 删除后，在添加以下内容：gnome-session &：

![7.png](https://img1.jcloudcs.com/cms/6ca88fcb-99cf-474f-b7fe-f05f8787a37020170808160541.png)

![8.png](https://img1.jcloudcs.com/cms/9bff8c9b-51b1-46d2-bc8b-3fc4157d03e020170808160630.png)

![9.png](https://img1.jcloudcs.com/cms/f7aad7c0-0e11-41c1-b4e8-61a90d375f6e20170808160803.png)

4.配置监听端口和环境参数，修改/etc/sysconfig/vncservers 文件，将最下方的两行配置注释，修改为以下内容：

vncservers="1:root" vncserverargs[1]="-geometry 1200x800"

![11.png](https://img1.jcloudcs.com/cms/af8fc52c-03a4-43e0-9217-28244db1aba020170808160924.png)

![12.png](https://img1.jcloudcs.com/cms/6b12ed3e-dcf3-4f8a-a295-d81d470288aa20170808160939.png)

5.重启服务使配置生效，执行：

service vncserver restart

![13.png](https://img1.jcloudcs.com/cms/5ab40aca-7a4b-4891-b841-8ecdb5874ba620170808161021.png)

**允许 root 访问图形界面和生成新的 machine-id**

执行以下命令：

sed -i 's/./*!= root./*//#&/' /etc/pam.d/gdmdbus-uuidgen >/var/lib/dbus/mechine-id

![1.png](https://img1.jcloudcs.com/cms/800857be-ca63-4bf5-850b-2d5a4789866820170809111548.png)

**关闭 selinux 和 NetworkManager 服务**

1.检查 selinux 服务并关闭，执行
vi /etc/selinux/config

确认里面的 SELINUX 字段的值是 disabled，如果不是则改为 disabled。

![20.png](https://img1.jcloudcs.com/cms/dad8fd8d-72a9-4b7b-8ab7-35288d186d8e20170808161446.png)

![19.png](https://img1.jcloudcs.com/cms/3cbd8694-137c-4194-a2de-7eb35ea08ae720170808161512.png)

2.关闭 NetworkManager 服务，执行

chkconfig --level 235 NetworkManager off

![17.png](https://img1.jcloudcs.com/cms/382cabcb-89b1-4847-bc1d-b74550e7f35720170808161627.png)

**测试登录成功**

![21.png](https://img1.jcloudcs.com/cms/5ee281e0-c1f6-4eb0-9719-4e913da3b78920170808161900.png)

![18.png](https://img1.jcloudcs.com/cms/80a79428-27e3-46ce-ad86-9a71084cc8bd20170808161938.png)

**CentOS7 安装 VNC Server**

**安装**

使用以下命令安装vncserver：

yum -y install tigervnc-server

![1.png](https://img1.jcloudcs.com/cms/ad8b24cd-de6d-4a85-96be-ceb82f64c16920170809094332.png)

**配置**

1.vi编辑配置文件，找到下面这几行，执行命令：

vi /lib/systemd/system/vncserver@.service

![0.png](https://img1.jcloudcs.com/cms/99cc2eaa-4945-4277-b275-71c18f43e9d420170809094503.png)

![2.png](https://img1.jcloudcs.com/cms/d837784e-ecf3-460c-ae04-c30776c662d020170809094546.png)

将Type更改为simple，用户名如果是root，那么<USER>就更改为root。

![3.png](https://img1.jcloudcs.com/cms/4b8f0822-5024-42c7-9abb-8fceae14077520170809094608.png)

2.将 /lib/systemd/system/vncserver@.service 改为 /lib/systemd/system/vncserver@:1.service，执行命令：

mv /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@:1.service

![4.png](https://img1.jcloudcs.com/cms/bf476dbe-fbdb-4ed1-8521-549bdb12222920170809095623.png)

3.重启 systemd，执行命令：

systemctl daemon-reload

![5.png](https://img1.jcloudcs.com/cms/4344d6eb-5dfc-4b92-a03c-9006236aec3b20170809095953.png)

4.设置 VNC 密码，要设置某个用户的密码，必须要有能通过 sudo 切换到用户的权限。如果当前用户已经有 root 这里我用 root 的权限，执行“直接vncpasswd”就可以了。

![6.png](https://img1.jcloudcs.com/cms/fc6d874d-66ee-4289-bd42-e60f74921f2320170809100141.png)

5.设置开机启动：

systemctl enable vncserver@:1.service

![7.png](https://img1.jcloudcs.com/cms/5665a53e-1455-4aa9-8505-13dc9d33cbb120170809100328.png)

启动服务：

systemctl start vncserver@:1.service

![8.png](https://img1.jcloudcs.com/cms/a7dfc3b0-ba27-45e9-b913-014a98ce677820170809100438.png)

**测试登录**

客户端连接 ，完成前述配置后，在客户端安装 VNC Viewer 等 VNC 客户端，然后输入服务器的 IP 地址加 VNC 端口号（默认为 5901），进行 VNC 的连接：

![9.png](https://img1.jcloudcs.com/cms/97d28a66-520c-4288-aebc-2e954a60df5d20170809100744.png)

如无法解决您的问题，请向我们提工单。