Windows服务器端口转发配置，可以使用Windows自带的portproxy功能实现，操作方法如下：

![image.png](https://img1.jcloudcs.com/cms/de68b960-58f0-4bb4-a2d9-9c71c7ebcc4c20180224091005.png)

此命令的含义是：

使用ipv4 to ipv4模式将源地址是116.196.123.136的22端口代理到本服务器的所有地址的12345端口上，源地址处也可以改为可以内网互通的服务器的内网地址。

可以通过show all来查看已经添加的端口转发的配置信息：

![image.png](https://img1.jcloudcs.com/cms/039d9b47-b90b-422b-b452-2aa669ba761720180224091029.png)

端口转发配置完成后，直接访问本机的公网地址的12345端口，实际访问的是116.196.123.136服务器的22端口。

如果想删除配置的转发策略，可以使用如下命令删除下：

![image.png](https://img1.jcloudcs.com/cms/c991c326-666b-44cc-93a3-a1020ea1d32020180224091124.png)