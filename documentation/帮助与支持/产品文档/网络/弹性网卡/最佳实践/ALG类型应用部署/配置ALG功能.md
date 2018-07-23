**配置ALG功能**

本部分将介绍使用iptables工具配置并模拟ALG功能，从而使FTP服务可以正常对外提供服务。

**步骤1**：通过FTP服务器的弹性公网IP地址进行SSH远程登录。

**步骤2**：执行以下命令进入配置网络目录。
/# cd /etc/sysconfig/network-scripts

**步骤3**：执行以下命令创建辅助IP配置文件。
/# touch ifcfg-eth0:0

**步骤4**：执行以下命令编辑辅助IP配置文件。

/# vi ifcfg-eth0:0

**步骤5**：在辅助IP配置文件中写入以下内容。
DEVICE=eth0:0 NM_CONTROLLED=yes ONBOOT=yes IPADDR=[secondary ip] NETMASK=[secondary ip netmask]

**步骤6**：执行以下命令编辑主IP配置文件。

/# vi ifcfg-eth0

**步骤7**：在主IP配置文件中修改以下内容。

BOOTPROTO=none IPADDR=[elastic ip] /#主网卡主IP对应的弹性公网IP NETMASK=255.255.255.255 GATEWAY=[primary ip gateway] /#主网卡的默认网关

**步骤8**：退出当前SSH连接，并使用辅助IP对应的弹性公网IP地址重新建立SSH连接

**步骤9**：执行以下命令重新启动网络服务
/# systemctl restart network

**步骤10**：执行以下命令添加原默认网关至eth0

/# ip route add [primary ip gateway] dev eth0

**步骤11**：通过iptables工具进行NAT转换配置

/# iptables -t nat -A PREROUTING -d [primary ip] -j DNAT --to-destination [elastic ip] /# iptables -t nat -A POSTROUTING -s [elastic ip] -j SNAT --to-source [primary ip]

**步骤12**：（可选）在路由表中添加辅助IP路由用于内部通信

/# ip route add [vpc cidr] via [primary ip gateway] src [secondary ip] dev eth0:0

**步骤13**：（可选）将步骤10-12的命令写入以下文件中以实现自动启动

/# cd /etc/rc.d /# vi rc.local

**步骤14**：（可选）修改rc.local文件权限

/# chmod +x /etc/rc.d/rc.local

**说明**

**[elastic ip]：主网卡主IP绑定的弹性公网IP**

**[primary ip gateway]：主网卡主IP对应的默认网关**

**[primary ip]：主网卡主IP**

**[secondary ip]：主网卡辅助IP**