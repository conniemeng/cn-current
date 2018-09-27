# **config**

Usage: jcloud config [OPTIONS]
Cloud user's access key and secret key.
--accesskey Access Key
--default-region Default Region Endpoint
--help Print usage
--secretkey Secret Key

您可以配置京东云账户的访问公钥和私钥。

1、默认使用区域请输入：cs-cn-north-2.jcloud.com:443；

2、Access Key请输入：[Access Key管理页面](https://uc.jcloud.com/account/accessKey)处于启用状态的Access Key ID；

3、Secret Key请输入：[Access Key管理页面](https://uc.jcloud.com/account/accessKey)处于启用状态的Access Key Secret；

4、Access Key认证证书默认保存在本地配置文件$HOME.\jcloud\config.json中；

5、配置Access Key时，如有任何问题 ，请您提交工单或联系客服。

![TimLine图片20170814110442.png](http://img1.jcloudcs.com/cms/5b3a8eba-e7b5-423c-aa61-f2cae77d256f20170814111256.png)

备注：

1. 
如您尚未生成Access Key，请参考[创建Access Key](https://www.jcloud.com/help/detail/595/isCateLog/1)；
1. 
请保留已授权的Access Key处于启用状态，其他Access Key置为禁用状态；
1. 
当前容器服务仅在华北地域开放。 其他机房上线时间请关注产品页说明；
1. 
公测期间，请您使用已授权的Access Key进行认证，如您需要更换Access Key，请联系客服重新授权；更换Access Key前请先将本地配置文件$HOME.\jcloud\config.json删除后，再验证新的Access Key。