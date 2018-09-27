# **安装CLI命令行工具******

1、打开控制台，选择“弹性计算->容器服务->实例->创建攻略”，单击“下载命令行工具”下面的“立即下载”，在弹出的页面上选择承载命令行工具运行的操作系统，即可完成命令行工具下载；

![TimLine图片20170808213423.png](https://img1.jcloudcs.com/cms/1c6cfc53-ab0a-4c01-9dc3-ba3aed675bc820170808213517.png)

或者，您也可以通过命令行完成命令行工具下载及安装过程；

* 
**以Windows为例，命令行工具下载及安装过程如下：**
1）打开安装包下载链接[http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-Windows-x86_64.zip](http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-Windows-x86_64.zip)，完成安装包下载；
2）对安装包进行解压缩操作；
3）打开windows命令行，运行.\jcloud.exe --help，其中.\前为jcloud.exe文件所在的绝对目录；
* 
**以Linuxs为例，命令行工具下载及安装过程如下：**
1）$ wget [http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-linux-x86_64.zip](http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-linux-x86_64.zip)
2）$ unzip jcloud-linux-x86_64.zip
3）$ chmod +x jcloud
4）$ ./jcloud --help[](https://jcloudcs.s-bj.jcloud.com/jcloud-Linux.zip)
* 
**以Mac为例，命令行工具下载及安装过程如下：**

1）$ curl -O [http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-mac-x86_64.zip](http://jcloudcs-hb.oss.cn-north-1.jcloudcs.com/jcloud-mac-x86_64.zip)
2）$ unzip jcloud-mac-x86_64.zip
3）$ chmod +x jcloud
4） ./jcloud --help

2、完成命令行工具安装后，在终端输入jcloud config，进行命令行工具的使用验证：

* 
默认使用区域请输入：cs-cn-north-2.jcloud.com:443；
* 
Access Key请输入：[Access Key管理页面](https://uc.jcloud.com/account/accessKey)处于启用状态的Access Key ID；
* 
Secret Key请输入：[Access Key管理页面](https://uc.jcloud.com/account/accessKey)处于启用状态的Access Key Secret。

![TimLine图片20170814110442.png](https://img1.jcloudcs.com/cms/5b3a8eba-e7b5-423c-aa61-f2cae77d256f20170814111256.png)

更多详情参考[jcloud config](https://www.jcloud.com/help/detail/612/isCateLog/1)说明。