该方法介绍通过为VPC中Linux系统的云主机配置SNAT，实现无公网云主机通过有公网的云主机代理访问公网。

注：SNAT的云主机单独一个子网

使用SSH的方法登录一个已经绑定了公网IP的云主机。

![image.png](https://img1.jcloudcs.com/cms/a9284cff-66b6-423b-b40d-93473c863dff20180427191038.png)

执行以下命令，开启IP转发功能。

sed -i 's/net.ipv4.ip_forward = 0/net.ipv4.ip_forward = 1/g' /etc/sysctl.conf

注意：如果表链的默认规则改成了drop，还需要执行以下命令。默认accept的情况，不需要执行此命令。

iptables -A FORWARD -d 10.242.1.0/24 -j ACCEPT

执行sysctl –p使IP转发生效。

![image.png](https://img1.jcloudcs.com/cms/d0f9a603-dcdb-4dbc-bd5f-588db92608ac20180427191054.png)

执行以下命令，为iptables添加SNAT转换

iptables -t nat -I POSTROUTING -s 10.242.0.0/16 -j SNAT --to-source 10.242.1.3

其中10.242.0.0/16是虚拟网络的网段，10.242.1.3是SNAT主机的内网IP

为内网主机单独创建一个路由表，路由策略如图

![image.png](https://img1.jcloudcs.com/cms/f5714246-49f6-478a-b361-a4b5bddf144620180427191108.png)

控制台vnc登陆一台只有内网的云主机10.242.0.3，实际测试已经可以访问公网了。

![image.png](https://img1.jcloudcs.com/cms/842fef3c-9dd4-4d46-8734-aca9c8369f4c20180427191119.png)