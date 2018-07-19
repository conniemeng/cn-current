**使用CloudBerry管理OSS**

**简介**

CloudBerry Explorer 是业界开发的一Windows 下直接通过 CloudBerry Explorer 来接入并管理对象存储的文件浏览器。您也可以通过CloudBerry Explorer来接入并管理京东云OSS。

CloudBerry主要功能包括：支持AK/SK登录，管理Bucket、管理Object、上传与下载、外链、同步等。

更多详细操作请下载**[《京东云对象存储CloudBerry使用手册》](https://oss.cn-north-1.jcloudcs.com/downloads/%E4%BA%AC%E4%B8%9C%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8CloudBerry%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.pdf)**

**使用CloudBerry接入OSS**

CloudBerry下载地址：[http://www.cloudberrylab.com/download-thanks.aspx?prod=cbes3free](http://www.cloudberrylab.com/download-thanks.aspx?prod=cbes3free)

使用 CloudBerry 之前，您需要事先在京东云中注册账号，并开通京东云对象存储服务（OSS）。

通过 CloudBerry 来接入 OSS 中的具体步骤如下。

步骤 1 在右侧的 Source 下拉菜单中点击“New Storage Account”，在弹框中选择S3 Compatible

![1.jpg](https://img1.jcloudcs.com/cms/36a860b9-df67-4508-86c5-005ee89e176320180208172913.jpg "1.jpg")

步骤 2 在弹出的对话框中，填写相应参数：

![2.jpg](https://img1.jcloudcs.com/cms/afdf2eda-15d5-4026-9b3d-f65fff16ed1d20180208172241.jpg)

Display name：显示名称，一般填自己的用户名即可。

Service point：填写京东云兼容S3的服务域名。（兼容S3服务域名详见[https://www.jdcloud.com/help/detail/1902/isCatalog/1](https://www.jdcloud.com/help/detail/1902/isCatalog/1)）

Access key、Secret key：接入 OSS 服务的 AK、SK。

Use SSL：是否使用 SSL。不勾选该选项。

Use native multipart upload（recommended）：是否使用分片上传

Signature version：选择4

步骤 3 单击“Test Connection”，测试是否能连接成功，或者直接单击“OK”进行连接。

![3.jpg](https://img1.jcloudcs.com/cms/5e841ff4-1b66-4171-b0e8-8953b36f384620180208172252.jpg)

连接成功之后，将看到账户（如 jcloud）下面对应的Bucket列表，如下图所示。

![4.jpg](https://img1.jcloudcs.com/cms/39c07179-2191-4c4a-8bf5-c2a4aed1d6c620180208172310.jpg "4.jpg")