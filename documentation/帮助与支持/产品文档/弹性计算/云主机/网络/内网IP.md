**内网IP**

京东云内网IP是无法通过Internet访问的IP地址，每个实例都具有分配内网IP的默认网络接口（eth0），京东云支持您为实例分配多个内网IP地址，分别为主内网IP及辅助内网IP，每一个内网IP均可以绑定一个弹性公网IP：

* 
主内网IP地址：随实例创建时由系统在指定的子网网段内自动分配的内网IP地址，不支持修改，不支持取消分配；
* 
辅助内网IP地址：实例创建后，除主内网IP外用户主动分配的内网IP，支持用户自定义IP地址或由系统自动分配，不支持修改，支持取消分配。

**使用限制**
**资源**

**限制**

**例外申请方式**每台云主机可分配的内网IP数

20

无法提额

注：实际可分配内网IP数还受限于云主机所在子网剩余可用IP数。

****

**分配辅助内网 IP**

1. 
打开控制台，选择[弹性计算>>云主机>>实例](https://console.jdcloud.com/host/compute/list)；
1. 
选定要分配内网IP的云主机，进入主机详情页，点击【云主机名称】—【主机详情】—【网络】Tab，查看已分配的内网IP及其对应绑定的公网IP；
1. 
点击【分配内网IP】在弹窗内添加需要分配的内网IP，可选择由系统自动分配内网IP地址，或自定义内网IP地址，需注意的是需要从当前云主机所在子网CIDR范围内指定，且不能与已占用地址冲突。支持同时分配多个；
1. 
点击“确定”则触发分配辅助内网IP。

注：在控制台操作完成后还需要登录云主机进行配置才能生效。

**Linux以CentOS 7.2为例详细操作如下：**

**方法一：**

1. 登录实例，详细请查阅[登录Linux实例](https://www.jdcloud.com/help/detail/360/isCateLog/1)

2. 执行命令
ip addr add [ip/mask] dev [devname] /#devname默认为 eth0

示例：若需要配置在子网 192.168.0.0/24 内的 IP 192.168.0.5，则只需执行命令

ip addr add 192.168.0.5/24 dev eth0

3. 完成内网 IP 配置配置

注：此种方式配置的内网 IP 仅写在实例系统内存中，实例重启后内网 IP 配置将失效，需要重新配置。

**方法二：**

1. 登录实例，详细请查阅[登录Linux实例](https://www.jdcloud.com/help/detail/360/isCateLog/1)

2. 执行命令
vim /etc/sysconfig/network-scripts/ifcfg-eth0

示例：若当前实例在控制台查询到的内网IP分别为192.168.0.4及192.168.0.5，其中192.168.0.4为主IP，文件内容显示：

TYPE="ETHERNET" BOOTPROTO="dhcp" DEFROUTE="yes" PEERDNS="yes" PEERROUTES="yes" IPV4_FAILURE_FATAL="no" IPV6INIT="yes" IPV6_AUTOCONF="yes" IPV6_DEFROUTE="yes" IPV6_PEERDNS="yes" IPV6_PEERROUTES="yes" IPV6_FAILURE_FATAL="no" NAME="eth0" UUID="dd73a4ea-8f6b-409b-a271-5f7882a3ae53" DEVICE="eth0" ONBOOT="yes"

修改为以下内容并保存：

TYPE="ETHERNET" /#BOOTPROTO="dhcp" DEFROUTE="yes" PEERDNS="yes" PEERROUTES="yes" IPV4_FAILURE_FATAL="no" IPV6INIT="yes" IPV6_AUTOCONF="yes" IPV6_DEFROUTE="yes" IPV6_PEERDNS="yes" IPV6_PEERROUTES="yes" IPV6_FAILURE_FATAL="no" NAME="eth0" UUID="dd73a4ea-8f6b-409b-a271-5f7882a3ae53" DEVICE="eth0" ONBOOT="yes" IPADDR0="192.168.0.4" IPADDR1="192.168.0.5" NETMASK1="255.255.255.0" NETMASK2="255.255.255.0" GATEWAY="192.168.0.1"

请注意，要将BOOTPROTO="dhcp"注释。

3. 重启网卡
systemctl restart network

4. 检查 eth0 网卡是否已经加入了 IP 地址

ip addr

5. 完成内网 IP配置

注：此种方式配置的内网 IP 在实例重启后依旧生效，但是如果为此实例制作自定义镜像后，基于此私有镜像创建的其他实例内网 IP 需要自行按照以上配置方法更新配置。

**Windows以Windows Server 2012 R2 标准版 64位 中文版为例**

1. 登录实例，详细请查阅登录Windows实例。若需要配置在子网 192.168.2.0/24 内的 IP 192.168.2.43（辅助IP），当前主内网IP为IP 192.168.2.42

2. 在左下角右键点击"开始"按钮，选择网络连接

![image.png](https://img1.jcloudcs.com/cms/d9fe3386-8989-4ef8-8fe5-a4b442980bf920171214205126.png)

3. 出现网络连接，右键点击后选择“属性”

![image.png](https://img1.jcloudcs.com/cms/66174772-1199-46fb-97a4-e605ee54133620171214205425.png)

4. 打开属性后，选择“Internet协议版本4（TCP/IPv4）”，点击“属性”

![image.png](https://img1.jcloudcs.com/cms/41f4e48f-249d-4e0b-9c2a-aa286c0b74f920171214205611.png)

5. 打开属性后，显示如下

![image.png](https://img1.jcloudcs.com/cms/2a589c7b-00a4-41b6-aeba-a2129883164f20171214205727.png)

将内容修改为下图所示后，再点击“高级”

![image.png](https://img1.jcloudcs.com/cms/92eb8dc3-e548-4e65-b96a-3fe76ddafd8720171214205948.png)

6. 点击高级后显示如下图

![image.png](https://img1.jcloudcs.com/cms/37c25dca-5e90-41a4-a856-ea1e06487ab520171218173638.png)

点击“添加”，按下图填写，点击“添加”确认

![image.png](https://img1.jcloudcs.com/cms/791e6b6f-4c17-4c75-8c20-18b2d8ec10c820171214210431.png)

点击“确认”回到属性页

![image.png](https://img1.jcloudcs.com/cms/35ea0fb0-2493-4e96-bc81-6c915afd00d720171214210233.png)

在DNS服务器地址处填写“103.224.222.222”及“103.224.222.223”后点击“确定”即设置完成

![image.png](https://img1.jcloudcs.com/cms/afcb0927-fee4-4fb7-979c-f64f329796e420171218174029.png)

**释放辅助内网 IP**

1. 
打开控制台，选择[弹性计算>>云主机>>实例](https://console.jcloud.com/host/compute/list)；
1. 
选定要释放内网IP的云主机，进入主机详情页，点击【云主机名称】—【主机详情】—【网络】Tab，查看已分配的内网IP及其对应绑定的公网IP；
1. 
选择需要释放的辅助内网IP，点击【释放】，请注意主内网IP不允许释放；
1. 
点击“确定”则触发取消分配指定的辅助内网IP。

注：主内网IP不支持释放。辅助内网IP释放时会自动解绑其绑定的公网IP，若您需要释放该公网IP，请至公网IP列表页进行操作。