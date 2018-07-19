**Windows系统SQL镜像登陆方法**

京东云部分Windows镜像系统自带微软SQL Server数据库，客户在第一次登陆SQL Server时可能会遇到无法登陆的情况；

![blob.png](https://img1.jcloudcs.com/cms/e716f1b2-df86-455c-ae65-9a75a0fb752a20170905141316.png)

![blob.png](https://img1.jcloudcs.com/cms/0c0f91b0-d1c2-485d-8289-5a877edd871120170905141537.png)

遇到这个问题需要您修改服务器名称需填“.”或当前实例名称

![blob.png](https://img1.jcloudcs.com/cms/1002bfb1-5347-47aa-acb4-0f7edb0d96b420170905141642.png)![blob.png](https://img1.jcloudcs.com/cms/ff0a420e-68a9-429c-81d5-19d9f7eb4d9d20170905141702.png)

默认情况下，SQL Server数据库的sa账号是禁用的，如果客户需要sa登陆管理；请在安全性--登录名中找到sa，右键选择属性后，在弹出界面选择已启用，并且设置相应账号和密码，下次登陆就可以使用sa了。

![blob.png](https://img1.jcloudcs.com/cms/abaf9978-e813-4e31-af9c-454384f3ae9120170905141835.png)