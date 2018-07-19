**Ubuntu配置图形界面和vnc**

注意：本文相关 Linux 配置及说明已在 Ubuntu14.04 64位操作系统中进行过测试。其它类型及版本操作系统配置可能有所差异，具体情况请参阅相应操作系统官方文档。

**安装gnome桌面环境：**

1.安装x－windows的基础，执行以下命令：
sudo apt-get -y install x-window-system-core

![1.png](https://img1.jcloudcs.com/cms/bfc0c5e1-46bc-4011-8fcf-0200a0867b0220170809151151.png)

2.安装登录管理器，执行以下命令：
sudo apt-get -y install gdm

![2.png](https://img1.jcloudcs.com/cms/dd16eb45-99fb-4c92-81b8-73ea9346ded920170809151241.png)

3.安装Ubuntu的桌面，执行以下命令：

sudo apt-get -y install ubuntu-desktop

![3.png](https://img1.jcloudcs.com/cms/52fde501-dbd1-4666-8ba4-554285fd5e1920170809151326.png)

4.进入图形界面，执行以下命令：

startx -extension GLX

![0.png](https://img1.jcloudcs.com/cms/da7b532e-84d2-420e-a7a0-e01eb11ced9f20170809151544.png)

**安装配置vncserver服务：**

****

**安装**

执行命令

apt-get -y install vnc4server

![4.png](https://img1.jcloudcs.com/cms/f3a965fc-dcd3-44de-ae77-45d71ee975e620170809151742.png)

**配置**

1.输入命令vncserver，开启 vnc服务。首次启动会要求设置密码，后面可以使用 vncpasswd 修改

![5.png](https://img1.jcloudcs.com/cms/13eac6b3-9c3d-4248-a00b-0bce411a2b4f20170809151908.png)

2.备份原有 xstartup 文件，执行命令：

cp /root/.vnc/xstartup /root/.vnc/xstartup.bak

![6.png](https://img1.jcloudcs.com/cms/bbacc712-4df4-406c-880e-a172860c102f20170809152101.png)

3.修改vnc启动文件，使用以下命令：

vi /root/.vnc/xstartup

![11.png](https://img1.jcloudcs.com/cms/842e1995-1b17-4c7e-8b50-767a86fb44ad20170809152529.png)

打开后如下图所示，把 x-window-manager &这一行注释掉，然后在下面加入一行 gnome-session &

![7.png](https://img1.jcloudcs.com/cms/89167243-13c4-417b-91d4-e583955aac1b20170809152752.png)

![8.png](https://img1.jcloudcs.com/cms/d12344be-d79a-4b6f-bd83-fe240c19e40f20170809152819.png)

4.杀掉原桌面进程，输入命令（其中的:1是桌面号），执行命令：

vncserver -kill :1

![9.png](https://img1.jcloudcs.com/cms/655cc27b-3c41-42cb-a88f-75963f98266720170809152933.png)

再次输入以下命令生成新的会话：

vncserver :1

![10.png](https://img1.jcloudcs.com/cms/a102c92c-a288-4f40-bc89-d14d27123b4c20170809153054.png)

5.设置vncserver开机自动启动，执行以下命令：

vi /etc/rc.local

![12.png](https://img1.jcloudcs.com/cms/e59cd361-922f-4f37-9e56-6c5ca98a8d0520170809164750.png)

添加vncserver启动命令 /usr/bin/vnc4server

![13.png](https://img1.jcloudcs.com/cms/9e0e4111-1cfb-4a96-bff0-83fe93db6b5820170809164842.png)

**测试登录**

客户端连接 ，完成前述配置后，在客户端安装 VNC Viewer 等 VNC 客户端，然后输入服务器的 IP 地址加 VNC 端口号（默认为 5901），进行 VNC 的连接：

![9.png](http://img1.jcloudcs.com/cms/97d28a66-520c-4288-aebc-2e954a60df5d20170809100744.png)

如无法解决您的问题，请向我们提工单。