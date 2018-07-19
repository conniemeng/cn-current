**登录Windows实例**

创建Windows类型的实例之后，您可以选择登录实例进行相关管理。根据您本地的操作系统和实例是否可被 Internet 访问，不同情况下可以使用不同的登录方式，具体内容可参考下表：
**本地操作系统类型**
 
**实例绑定公网****IP**
 
**实例没有绑定公网****IP** Windows
 
VNC 登录
远程桌面连接
 
VNC登录 Linux
 
VNC 登录
rdesktop登录 Mac OS
 
VNC 登录
rdesktop登录

### **登录准备**

创建实例并获取账号和对应密码。

管理员账号：Administrator

密码：京东云实例可以通过两种方式获取密码

* 
在创建实例时，选择“暂不设置”，则系统将以短信及邮件方式发送默认密码，您可以在登录实例时，使用默认密码进行验证。
* 
选择“立即设置”，则在密码设置文本框中输入自定义密码，如果忘记密码，可以通过“[重置密码](http://www.jdcloud.com/help/detail/335/isCateLog/1)”功能重新设置密码，此功能只有“运行”状态主机可用。

### **使用 VNC 登录云主机**

VNC登陆是京东云为用户提供的一种通过 Web 浏览器远程连接实例的方式。在没有安装远程登陆客户端或者客户端远程登陆无法使用的情况下，用户可以通过 VNC 登陆连接到实例，观察实例状态，并且可通过实例账户进行基本的云服务器管理操作。

VNC登陆的场景至少包括以下几种:

* 
查看实例的启动进度
* 
无法通过客户端 SSH 或 mstsc 登录时，通过 VNC 登陆来登录实例

1.在云服务器列表的操作列，点击【远程连接】登录图标按钮即可通过 VNC 连接至 Windows 实例。

![image.pndg](https://img1.jcloudcs.com/cms/af21f118-d512-4816-9b5c-a3dfca9fc78720171207160642.png)

2.通过在左上角点击 Ctrl+Alt+Del 命令进入系统登录界面：

![](https://img1.jcloudcs.com/cms/83d9ca92-8243-4f18-b28c-b326cee1825f20170324192709.png)

### ****

请注意：

* 
同一浏览器下，同一时间只支持使用VNC登录一台云主机录。
* 
要正常使用VNC登录，建议使用高版本浏览器，如：Chrome，Firefox，IE10及以上版本等。
* 
暂不支持复制粘贴。
* 
暂不支持文件上传下载。

### **本地为Windows，使用远程桌面登录Windows云主机**

使用MSTSC 远程桌面连接Window云主机，须先确保主机绑定公网IP，并且安全组和网络ACL规则中允许通过此类访问。可在京东云控制台创建Windows系统实例，获得公网IP：XXX.XXX.XXX.XXX

1.点击电脑【开始】按钮，找到“运行”

![](https://img1.jcloudcs.com/cms/e6561615-702d-45f1-a4d8-80e04bed28bc20170324192221.png)

2.在运行中输入mstsc命令，点击确定，即可打开远程桌面连接对话框。

![](https://img1.jcloudcs.com/cms/eebb8134-d68e-4bc2-892d-3f14fd0e841420170324192245.png)

3.根据创建实例时绑定的公网IP，连接实例，输入用户名：Administrator，勾选“允许我保存凭据”。

![a.png](https://img1.jcloudcs.com/cms/1a652720-a2a5-43c2-be51-3065266958a220170728193346.png)

4. 点击“连接”后，输入密码，连接到京东云实例。

![b.png](https://img1.jcloudcs.com/cms/e76cae1d-ef11-4643-8724-f3e14e4cddf720170728193459.png)

5.勾选“不再询问我是否连接到此计算机”点击“是”。

![](https://img1.jcloudcs.com/cms/31572008-6363-49fb-bd11-908cf87a608120170324192437.png)

6.成功连接到您在京东云创建的实例

如果登录失败，请确认公网IP地址是否输入正确，并查看安全组和网络ACL配置，请检查您的实例是否允许3389端口的入流量。

![c.png](https://img1.jcloudcs.com/cms/dfbb5b45-8380-49a0-a504-ab604e50e99920170728193533.png)

**本地为Linux，使用rdesktop登录Windows云主机**

本地系统为Linux，需要远程登录Windows云主机时，需要安装相应的远程桌面连接程序，通常使用rdesktop客户端。

登录之前请您查看主机所在[安全组](http://www.jdcloud.com/help/detail/744/isCateLog/1)及所在子网的[网络ACL](http://www.jdcloud.com/help/detail/1512/isCateLog/1)配置，确保云主机3389端口已开放。在安装了rdesktop之后，运行以下命令登录云主机
rdesktop -u administrator -p <云主机登录密码> <云主机公网IP地址>