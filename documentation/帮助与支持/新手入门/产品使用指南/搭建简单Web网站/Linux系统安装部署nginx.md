1.清除yum缓存：yum clean all；（可选步骤）

2.重新安装yum：yum makecache；（可选步骤）

3.更新yum：yum update；

4.安装nginx ：yum install nginx；

5.重新启动nginx:service nginx restart

6.本地浏览器中输入外网IP，出现如下页面，则nginx安装成功

![](https://img1.jcloudcs.com/cms/888504f3-769f-4034-8933-dcc15f9ccbe020170313112919.png)****

7.前往nginx的默认登录页目录：cd /usr/share/nginx/html

8.使用VI编辑器，修改index.html文件：vi index.html；

9.修改index.html文件内容，完成后按Esc输入“：wq”保存退出；

![](https://img1.jcloudcs.com/cms/e9bc0363-65a6-4402-81ca-e5acd7ec535d20170313112931.png)

10.重新启动nginx:service nginx restart,在本地浏览器中输入外网IP，出现如下页面，则基于nginx服务器的静态页面网站搭建成功。

![](https://img1.jcloudcs.com/cms/2f2ead58-73ac-4221-9850-77a63b81740920170313112943.png)

至此，您已经在京东云上成功部署了Web环境，可以制作和发布站点了。