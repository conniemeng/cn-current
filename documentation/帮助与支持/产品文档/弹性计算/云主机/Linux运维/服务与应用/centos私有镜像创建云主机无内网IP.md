**使用centos私有镜像创建云主机后无法获取内网IP解决办法**

有时使用之前制作的centos私有镜像创建云主机后发现云主机未获取内网IP，ifconfig -a查看网络信息发现网卡名称变为eth1，且没有内网IP信息，如图所示：

![noip.JPG](https://img1.jcloudcs.com/cms/c544238a-baa1-4266-a8da-a2dc73def19b20171230160357.JPG)

这是由于创建私有镜像时保留了网卡的UUID信息，导致使用私有镜像创建云主机时，系统自动分配网卡为eth1，而/etc/sysconfig/network-scripts下又没有ifcfg-eth1配置文件（只有原有的ifcfg-eth0文件），导致系统有eth0的配置文件但找不到eth0设备，有eth1设备但没有eth0配置文件，所以无法获取内网IP，同时公网IP也无法访问。

解决办法：

执行vi /etc/udev/rules.d/70-persistent-net.rules如图所示：

![rules.JPG](https://img1.jcloudcs.com/cms/60fdd35e-4ac1-4a2e-9618-45744b8abc7d20171230161102.JPG)

可以看到系统在原有eth0网卡的内容（红框）下自动生成了eth1的内容（黄框）。

修改文件，将eth0部分的内容注释掉，将eth1内容中的设备名改为eth0，如下图两处红框所示，wq保存文件并退出。

![rules2.JPG](https://img1.jcloudcs.com/cms/ce1effb3-9044-45be-afd5-b7ab7fd4e8bc20171230161140.JPG)

reboot重启云主机，重启后，执行ifconfig -a发现之前的eth1设备名恢复为eth0且可以获取内网IP，绑定公网IP后也可以正常访问，如图：

![ifconfig -a.JPG](https://img1.jcloudcs.com/cms/2c606be3-5b02-4602-9a61-84d075ef8de620171230161157.JPG)

如无法解决您的问题，请向我们提工单。