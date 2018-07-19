**登录Linux实例**

在购买并启动了 Linux 类型的实例后，您可以连接并登录它。根据您本地的操作系统和实例是否可被 Internet 访问，不同情况下可以使用不同的登录方式，具体内容可参考下表：
**本地操作系统类型**

**Linux云主机绑定公网IP**

**Linux云主机没有绑定公网IP**Windows

VNC 登录
远程登录软件登录

密钥登录

VNC登录Linux

VNC 登录
SSH登录

密钥登录Mac OS

VNC 登录
SSH登录

密钥登录

###

### **登录准备**

创建实例并获取账号和对应密码

管理员账号：root

密码：京东云实例可以通过两种方式获取密码

* 
在创建实例时，选择“暂不设置”，则系统将以短信及邮件方式发送默认密码，您可以在登录实例时，使用默认密码进行验证。
* 
选择“立即设置”，则在密码设置文本框中输入自定义密码，如果忘记密码，可以通过“[重置密码](http://www.jdcloud.com/help/detail/335/isCateLog/1)”功能重新设置密码，此功能只有“运行”状态主机可用。

### **使用 VNC 登录云主机**

VNC登录是京东云为用户提供的一种通过 Web 浏览器远程连接云主机的方式。在没有安装远程登陆客户端或者客户端远程登陆无法使用的情况下，用户可以通过 VNC 登陆连接到实例，观察实例状态，并且可通过实例用户进行基本的实例管理操作。

VNC登陆的场景至少包括以下几种:

* 
查看实例的启动进度
* 
无法通过远程登录软件或密钥登录时，通过 VNC 登陆来登录实例

1. 
在列表的名称列，点击【远程连接】即可通过 VNC 连接至Linux实例

![image.png](https://img1.jcloudcs.com/cms/ab834664-93f0-4223-a75a-bdd7d67a788120171207160611.png)
1. 
点击VNC之后进入到登录页面

默认用户名：root

密码为您创建实例时设置的实例密码

![](https://img1.jcloudcs.com/cms/8d833622-4afa-447c-b893-effa7d7ad5ac20170324193305.png)

请注意：

* 
同一浏览器下，同一时间只支持使用VNC登录一台云主机录。
* 
要正常使用VNC登录，建议使用高版本浏览器，如：Chrome，Firefox，IE10及以上版本等。
* 
暂不支持复制粘贴。
* 
暂不支持文件上传下载。

### ****

### **本地为Windows，使用密码登录Linux云主机**

您可选择多种远程登录软件登陆京东云Linux云主机，本例以 CentOS 7.1 64位系统，Xshell远程登录软件为示范，可按照如下步骤完成登录。

1. 下载并安装远程登录软件

可使用此地址下载：[http://iaas-cns-download.s3.cn-north-1.jcloudcs.com/xshell5_5.0.1332.exe](http://iaas-cns-download.s3.cn-north-1.jcloudcs.com/xshell5_5.0.1332.exe)或自行下载Xshell软件

下载后双击xshell5_5.0.1332.exe进行安装

2. 安装完成，打开Xshell，并点击新建，根据要求输入相应参数

名称：自定义设置

协议：SSH

主机：实例所绑定的公网IP，可在实例列表查询

端口号：22

![1.png](https://img1.jcloudcs.com/cms/eb224958-7a61-40db-8919-b4fcebecc0da20170728191925.png)

3.选择用户身份认证

方法选择：Password

用户名：默认用户名为root

![](https://img1.jcloudcs.com/cms/c02dbc8e-70a3-41f2-b716-92dffabff59320170324193025.png)

4.点击确定，连接云主机，如下图：

![2.png](https://img1.jcloudcs.com/cms/5c4356e5-5c94-4a8d-b121-f97820f7dae620170728192536.png)

****

**本地为Windows，使用SSH密钥登录****Linux****云主机**

使用SSH密钥登录云主机，需要在创建云主机时选择开启密钥登录功能，并为其绑定一个密钥，请确保已下载所绑定密钥的私钥。有关密钥的创建操作，请参阅[创建密钥](http://www.jdcloud.com/help/detail/330/isCateLog/1)。

同时请您查看主机所在[安全组](http://www.jdcloud.com/help/detail/744/isCateLog/1)及所在子网的[网络ACL](http://www.jdcloud.com/help/detail/1512/isCateLog/1)配置，确保云主机22端口已开放。

您可选择多种远程登录软件登陆京东云Linux云主机，本例以 CentOS 7.1 64位系统，Xshell远程登录软件为示范，可按照如下步骤完成登录。

1.下载并安装远程登录软件

可使用此地址下载：[http://iaas-cns-download.s3.cn-north-1.jcloudcs.com/xshell5_5.0.1332.exe](http://iaas-cns-download.s3.cn-north-1.jcloudcs.com/xshell5_5.0.1332.exe)或自行下载Xshell软件[](http://rj.baidu.com/soft/detail/15201.html?ald)

下载后双击xshell5_5.0.1332.exe进行安装

2.安装完成，打开Xshell，并点击新建，根据要求输入相应参数

名称：自定义设置

协议：SSH

主机：主机公网IP

端口号：22

![QQ截图20170728192105.png](https://img1.jcloudcs.com/cms/a64d63d8-de9c-4295-bb0c-b0a9e889124620170728192124.png "QQ截图20170728192105.png")

3.进行用户身份认证

点击左侧“类别”中的【用户身份验证】，根据要求输入相应参数

方法：选择Public Key

用户名：默认用户名为root

用户密钥：点击【浏览】-->【导入】，打开弹窗后找到本地保存的私钥，点击【打开】，返回用户密钥配置窗口。

![](https://img1.jcloudcs.com/cms/d9d99066-23ac-4029-bcc1-61e02bed97e720170410110610.png)

选中导入的密钥后，点击【确定】，可以看到该密钥显示在“用户密钥”处。再次点击【确定】。

![](https://img1.jcloudcs.com/cms/39d43ca7-2559-43b3-9fac-afa50ecb768220170410110639.png)

在会话连接确认窗口中，选择【连接】，选择以何种方式接受实例密钥。

![4.png](https://img1.jcloudcs.com/cms/e27bdb25-da9a-4497-92e8-0db48dbf238720170728192759.png)

若连接成功，显示如下图，若连接失败，请确认公网IP地址是否输入正确，并查看安全组和网络ACL配置。

![5.png](https://img1.jcloudcs.com/cms/ff983ccf-8e01-4c64-a0a4-b0b58f8deca720170728192837.png)

****

**本地为Linux/Mac OS，使用SSH登录****Linux****云主机**

Linux用户请直接运行以下命令，Mac OS用户请打开系统自带的终端（Terminal）后运行以下命令：
ssh root@<云主机的公网IP地址>

随后输入该主机root用户的密码，输入正确即可连接实例

### **本地为Linux/Mac OS，使用密钥登录****Linux****云主机**

Linux用户请直接运行以下命令，Mac OS用户请打开系统自带的终端（Terminal）后运行以下命令，以对私钥文件赋予本人可读的权限：
chmod 400 <下载到本地的与云主机绑定的私钥绝对路径>

随后运行以下远程登录命令:

ssh -i "<下载到本地的与云主机绑定的私钥绝对路径>" root@<云主机公网IP地址>