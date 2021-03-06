**创建Windows实例**

**前提条件**

在创建Window实例前，您需要完成以下步骤

* 
注册京东云账号并激活、认证账号，可分别访问[注册京东云](https://uc.jdcloud.com/reg)、[登录京东云](https://uc.jdcloud.com/login)、[实名认证](https://uc.jdcloud.com/account/certify)进行操作；
* 
若您需要创建按配置计费实例，您需要保证您的余额不低于50元，若当前余额不足请进行[充值](https://uc.jdcloud.com/user/recharge_index)；
* 
您可预先创建[私有网络](http://www.jdcloud.com/help/detail/1527/isCateLog/1)、[子网](http://www.jdcloud.com/help/detail/1542/isCateLog/1)或随实例一起创建私有网络及子网；
* 
若您需要使用安全组进行实例的安全访问控制，您可预先[创建安全组](http://www.jdcloud.com/help/detail/1486/isCateLog/1)、配置安全组或随实例一起。

**操作步骤**

1. 
打开控制台，选择[弹性计算>>云主机>>实例](http://console.jdcloud.com/host/compute/list?dataCenter=bj_02)
1. 
选择创建云主机所属地域，点击“创建”按钮，进入[云主机购买页面](http://console.jdcloud.com/host/compute/create?dataCenter=bj_02)建议您根据业务情况选择实例所在地域，关于京东云地域详细信息请查阅[地域](http://www.jdcloud.com/help/detail/872/isCateLog/1)。![image.png](http://img1.jcloudcs.com/cms/797bf42a-cd80-4e3a-a1ce-7e2d62ba0f8120171207155450.png)
1. 
选择计费模式：包年包月和按配置计费，包年包月按一个正月进行购买付费，按配置计费按照实际使用的时长（精确至秒）进行计费。关于两种计费方式的区别，请查阅[计费规则](http://www.jdcloud.com/help/detail/290/isCateLog/1)。![按配置.png](https://img1.jcloudcs.com/cms/236ef762-7da8-456a-8d12-ab779473ebea20170728154141.png)
1. 
地域与可用区选择：在此步骤仍可以选择云主机对应的地域（华北-北京、华南-广州、华东-宿迁及华东-上海）及可用区，请注意“不同地域资源内网不互通，创建之后不可更改”，如果所选地域限额已满，可以通过[提交工单](https://uc.jdcloud.com/question/submit)提升限额。

![image.png](https://img1.jcloudcs.com/cms/3f8073fe-d063-47e1-8fbf-3cdff711b21b20180124183828.png)
1. 
选择镜像：

京东云为您提供以下镜像类型：

**官方镜像**官方镜像是由京东云提供和维护的公共镜像，支持Linux和Windows的多个发行版本，提供基础操作系统、初始化组件及部分预装软件，所有用户均可以使用。
**私有镜像**
私有镜像是基于用户自有云主机创建自定义镜像，您可以为已部署业务的主机制作镜像，基于此镜像快速创建多个具有相同配置和软件环境的主机。您可以将私有镜像共享给同其他京东云用户，被共享镜像会显示在目标用户同区域的共享镜像列表中。私有镜像支持删除和基本信息修改。
**共享镜像**
共享镜像是由其他京东云用户通过镜像共享功能所分享而来的用户自定义镜像，展示区域与被共享的私有镜像相同。共享镜像仅可用于创建云主机，不可进行基本信息修改、删除等操作，若发起共享的用户取消了共享，则该镜像会从列表中自动删除。
**镜像市场镜像**
镜像市场镜像是由入驻云市场的服务商所提供的镜像，集成了针对不同业务场景的运行环境或软件，方便用户快速部署业务。

对于初次使用京东云的用户可以选择京东云提供的“官方镜像”，您可以根据需要选择对应的系统，并选择合适的版本。如果您已经创建好自己的实例，并配置好相应的环境，可以将此实例进行制作私有镜像操作，同时基于此镜像批量创建有相同系统及环境配置的主机，还可以将此私有镜像共享给其他京东云用户。

![image.png](https://img1.jcloudcs.com/cms/b791a4b6-404a-4988-8248-ed1e03433b8d20180130004140.png)
1. 
京东云云主机的配置支持用户自定义选择：从最小的1核1G到32核128G，用户可以根据不同业务场景选择实例规格及相应配置，详细请查阅[实例规格类型](http://www.jdcloud.com/help/detail/302/isCateLog/1)。

![image.png](https://img1.jcloudcs.com/cms/2c46efcf-595a-43a7-9323-377301c1b95920180130004244.png)
1. 
云主机存储：京东云提供云硬盘和本地硬盘两种类型。

云硬盘：采用一盘多备的分布式存储方式，数据可靠性高

本地盘：处在云服务器所在的物理机上的存储设备，可以获得较低的时延，但存在单点丢失风险。

云主机系统盘：仅支持本地盘，赠送40GB。

云主机数据盘：支持挂载四块数据盘，可选高效云盘和SSD云盘，云硬盘挂载到云主机后，需要进入云主机操作系统[挂载云硬盘](http://www.jdcloud.com/help/detail/319/isCateLog/1)。

高效云盘做数据盘：支持范围20G~3000G

SSD云盘做数据盘：支持范围20G~1000G

您可以随实例创建指定类型和容量的空盘，也可以基于已有云硬盘快照创建数据盘（基于快照创建的数据盘类型暂不支持调整，容量调整范围下限为快照容量），如您选择的私有镜像中包含了预设的数据盘配置信息，则选择私有镜像后会自动按照镜像中的设备映射信息配置数据盘，如您仅希望使用镜像的部分默认配置，也可以对其进行删减（不支持在默认配置上更换快照，如欲更换快照请删除默认配置后单独添加新盘后选择快照）。关于数据盘设备名分配规则请查阅[硬盘价格](http://www.jdcloud.com/help/detail/864/isCateLog/1)。

![主机创建-数据盘.png](https://img1.jcloudcs.com/cms/153decee-6062-44fa-9f8d-fc5b900d177f20180322215830.png)
1. 
云主机网络

选择“私有网络”及“子网”，选择子网后，可以判断该子网下，还有可以创建的云主机数量，如果暂时没有子网，可以通过快速入口新建子网，并在“云主机网络”进行选择，详细请查阅[](http://www.jdcloud.com/help/detail/464/isCateLog/1)[私有网络](http://www.jdcloud.com/help/detail/1509/isCateLog/1)和[子网](http://www.jdcloud.com/help/detail/1510/isCateLog/1)。

选择对应的已创建的安全组，安全组为必选项，安全组也可以通过快速入口创建，详细请查阅[创建安全组](http://www.jdcloud.com/help/detail/1486/isCateLog/1)，完成创建后，在“网络”进行选择。

![选择子网.png](http://img1.jcloudcs.com/cms/e629d048-2bb1-475c-a439-0dbef1e9072b20170728155557.png)
1. 
云主机带宽：

京东云提供的公网IP带宽类型为按固定带宽计费及按使用流量计费，按固定带宽计费按购买时设置的带宽上限值计费，而与您实例当前实时访问公网带宽无关，按使用流量计费则根据您实时访问公网的实际流量计费。线路分为：BGP和非BGP，若您需要更快更高效的网络接入请选用BGP。

带宽范围为：1Mbps~200Mbps，在创建主机过程中可以暂不购买公网IP，完成主机创建后，再进行绑定。

公网IP带宽费用与实例费用独立。具体价格信息请查阅[公网IP价格](http://www.jdcloud.com/help/detail/868/isCateLog/1)。
**实例计费方式** **公网带宽计费方式** **费用估算** 按配置 按固定带宽 配置费用，包括：实例规格（CPU 和内存的配置）、数据盘（如果有）、和公网IP带宽的费用。 按使用流量 公网流量费用 + 配置费用。其中，配置费用包括：实例规格（CPU 和内存的配置）、数据盘（如果有）的费用及公网IP配置费。 包年包月 按固定带宽 配置费用，包括：实例规格（CPU 和内存的配置）、数据盘（如果有）、和公网IP带宽的费用。 按使用流量 公网流量费用 + 配置费用。其中，配置费用包括：实例规格（CPU 和内存的配置）、数据盘（如果有）的费用及公网IP配置费。

![带宽.png](http://img1.jcloudcs.com/cms/c99ba72e-370b-4881-a32b-b4f08aa980f920170728152933.png)
1. 
设置主机名、描述、密码及登录方式

首先您需要设置创建的主机名，名称不可为空，只支持中文、数字、大小写字母、英文下划线“_”及中划线“-”，且不能超过32字符，如果为批量创建购买，名称会以“xxx1”、“xxx2”依次显示。

对于设置密码，可以选择“立即设置”密码，也可以选择“暂不设置”（系统会以短信和邮件方式发送默认密码）

![image.png](https://img1.jcloudcs.com/cms/91154fd5-a370-49d3-9e57-ca850c53762f20170913174133.png) 对于Windows系统，不支持使用SSH密钥登录。

11.确认云主机数量及购买时长

购买数量受限于该地域您云主机、云硬盘、公网IP限额以及所选子网剩余IP数量，若限额不够，可通过[提交工单](https://uc.jcloud.com/question/submit "提交工单")提升限额。

若购买包年包月实例，则需要设置购买时长，最短为1个月，最长为2年，花十个月价钱即可享受一年服务。若需要更长服务时长请[提交工单](https://uc.jcloud.com/question/submit "提交工单")。

![](https://img1.jcloudcs.com/cms/9762a0f1-663b-4c1b-90a0-1087fad6838520170410100715.png)

12.完成云主机相关配置之后，点击【立即购买】完成支付后即可进入[控制台](http://console.jcloud.com/host/compute/list?dataCenter=bj_02 "控制台")查看创建的云主机。

![主机列表.png](https://img1.jcloudcs.com/cms/9598a1c3-2c5e-4764-90c7-73e9d817accf20180322220717.png)

****