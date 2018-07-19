Linux系统中/etc/ssh/sshd_config 下有两个参数可能会导致ssh连接慢，分别是UseDNS 和GSSAPIAuthentication，如遇到ssh登陆慢的问题，请参考如下操作：

编辑配置文件 /etc/ssh/sshd_config， vi /etc/ssh/sshd_config 找到 UseDNS选项，如果没有注释，将其注释 /#UseDNS yes 添加 UseDNS no

![blob.png](https://img1.jcloudcs.com/cms/30bcf9cf-3f46-4837-afaf-d7e8bf73fcf420180428131110.png)

2、找到 GSSAPIAuthentication选项，如果没有注释，将其注释 /#GSSAPIAuthentication yes 添加 GSSAPIAuthentication no

![blob.png](https://img1.jcloudcs.com/cms/0b3cd573-5eb9-4d9a-aa0b-ed54901f1e7520180428131133.png)

3、保存配置文件

重启SSH服务 /etc/init.d/sshd restart

注：如果客户端为Linux系统，需确保客户端做同样修改并重启生效。