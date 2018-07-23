1.清除yum缓存：yum clean all；（可选步骤）

2.重新安装yum：yum makecache；（可选步骤）

3.更新yum：yum update；

4.安装httpd ：yum install httpd；

5.前往httpd的默认登录页目录：cd /var/www/html；

6.使用VI编辑器，编辑index.html文件：vi index.html；

7.编辑index.html文件内容，完成后按Esc输入“：wq”保存退出；

![](https://img1.jcloudcs.com/cms/2b3a3f69-17a3-4b84-947d-d824f7551f8e20170313112805.png)

8.启动httpd服务：service httpd start；

9.在本地浏览器中访问网站的公网IP，可以看到Apache服务器配置成功。

![](https://img1.jcloudcs.com/cms/555c9c64-ff7f-4a4b-93ca-4642b0af808320170313112812.png)

至此，您已经在京东云上成功部署了Web环境，可以制作和发布站点了。