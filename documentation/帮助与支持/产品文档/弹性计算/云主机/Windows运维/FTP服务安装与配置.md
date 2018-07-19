**FTP服务安装与配置**

使用云主机的过程中，我们经常遇到想要上传文件到主机中或者下载文件到本地的情况，这时我们需要用到FTP服务。

FTP 是File Transfer Protocol（文件传输协议）的英文简称，而中文简称为“文传协议”，用于Internet上的控制文件的双向传输。同时，它也是一个应用程序（Application）。基于不同的操作系统有不同的FTP应用程序，而所有这些应用程序都遵守同一种协议以传输文件。本文详细介绍Windows Server系统环境下，如何部署和使用FTP服务来进行文件的上传和下载。

**一、安装前准备**

本文安装环境为windows server 2008 R2 企业版 64位中文版的系统，京东云官方镜像中提供了此镜像，选用此镜像创建云主机后，远程连接登录到系统中。

**二、安装FTP**

1、安装IIS/FTP角色。

开始——>管理工具——>服务器管理器

![](https://img1.jcloudcs.com/cms/b4ab5ffd-55ba-4ea8-8ed5-ac11ddaeca0d20170424210425.png)

点击角色——>添加角色

![](https://img1.jcloudcs.com/cms/c9839306-0db6-4858-86f9-23b600ef6ccc20170424210506.png)

弹出添加角色对话框，选择下一步

![](https://img1.jcloudcs.com/cms/0da65962-492b-4d16-91ea-c43b6427cf3120170424210531.png)

选择Web服务器（IIS），点击下一步

![](https://img1.jcloudcs.com/cms/01a3d1fd-b41f-4ef9-934a-caafd991315920170424210551.png)

点击下一步

![](https://img1.jcloudcs.com/cms/27aa8f11-9a3b-44ab-99c7-10c58b327fbd20170424210605.png)

然后选择FTP服务，点击下一步

![](https://img1.jcloudcs.com/cms/ec43f1ee-1eed-466c-abf2-d26bb222db1220170424210734.png)

确认无误后点击安装，直到安装结束

![](https://img1.jcloudcs.com/cms/efb380b9-8346-4e9e-9eb3-efc606c43cbd20170424210832.png)

点击开始——>管理工具——>IIS管理器

![](https://img1.jcloudcs.com/cms/8602725d-0013-4345-9a51-618df77bdfb620170424210925.png)

右键点击网站，如果能够出现创建FTP站点，则表明FTP服务安装成功

![](https://img1.jcloudcs.com/cms/784b2cbd-f5b3-4842-bfb2-90c1c1dafabd20170424210944.png)

2、创建Windows用户名和密码，用于FTP使用。

开始——>管理工具——>服务器管理器，添加用户，如下图：本实例使用ftptest。

![](https://img1.jcloudcs.com/cms/15b1ff9b-daa0-452b-b887-cb7c31b9087c20170424211126.png)

在设置密码时要采用大写字母加小写字母加数字的组合,否则会显示无法通过密码策略。点击创建，即可成功创建新用户ftptest。

![](https://img1.jcloudcs.com/cms/3f898605-5fe5-4f0e-ab31-67c67338fc0920170424211213.png)

创建成功如下图。

![](https://img1.jcloudcs.com/cms/fcd86f52-6236-40b1-8f2b-ea9851631a7d20170424211230.png)

3、配置FTP站点。

在服务器磁盘上创建一个供FTP使用的文件夹，创建FTP站点，指定刚刚创建的用户ftptest，赋予读写权限。

右键点击网站——>添加FTP站点

![](https://img1.jcloudcs.com/cms/af9973e2-3338-40c0-be7d-f7b85ffd491020170424211310.png)

填写FTP站点名称与默认目录。

![](https://img1.jcloudcs.com/cms/2a7dff9d-23e7-470a-9504-64ea2ce7e8d420170424211340.png)

绑定21端口(也可自行设置)。

![](https://img1.jcloudcs.com/cms/818b9ad2-fc96-4a13-8ed2-c2acaf93e68d20170424211405.png)

授权之前创建的ftptest用户允许访问和读写权限。

![](https://img1.jcloudcs.com/cms/9d30acf2-e4f5-43ba-b09f-2a950442c9fc20170424211507.png)

设置完成后如下图所示，Ftptest即为新配置的站点。

![](https://img1.jcloudcs.com/cms/eb5c92fb-6be6-4fb1-9662-e72764fc42dd20170424211531.png)

4、客户端测试。

直接使用地址ftp://服务器ip地址:ftp端口(如果不填端口则默认访问21端口)，如图。弹出输入用户名和密码的对话框表示配置成功，正确的输入用户名和密码后，点击登录，即可对FTP文件进行相应权限的操作。

![](https://img1.jcloudcs.com/cms/cf184599-5877-4c57-b079-8191f3e1b06820170424211542.png)

如在FTP站点中创建test文件夹如下。

![](https://img1.jcloudcs.com/cms/4247c946-f7ff-4de8-b0cb-8eb1e45fdd7f20170424211601.png)

****

**三、问题解读**

服务器无法连接

![](https://img1.jcloudcs.com/cms/0dc0bb9f-80d1-4c27-80c9-2bc49d8f737820170424211641.png)

排查方法如下:

1、 本地电脑尝试telnet服务器21端口是否有响应

![](https://img1.jcloudcs.com/cms/55a2de74-f2ee-49a5-aae2-05e5435db4c420170424211723.png)

如果没有响应说明可能FTP服务没有启动，或者服务器防火墙限制了通信。

检查FTP服务器是否启动：登陆服务器后可以使用netstat–an | findstr :21 查看21端口是否被监听

![](https://img1.jcloudcs.com/cms/0b698963-f9a9-46ec-8c3c-242ec8070c8320170424211831.png)

启动FTP后再次执行netstat–an | findstr :21查看已经监听正常。

![](https://img1.jcloudcs.com/cms/17fc8734-870b-4011-bf39-4c7a21151efd20170424211848.png)

2、 检查防火墙是否放行21端口，如果不确定可以先尝试关闭防火墙，在运行中输入firewall.cpl可以进行设置。

![](https://img1.jcloudcs.com/cms/b318db78-6e8e-4ede-835c-f1074283df5520170424211929.png)

经过上述步骤测试已经正常。