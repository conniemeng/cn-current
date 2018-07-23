# **多主机共享公网IP**

**目的**：实现相同VPC下的多台主机通过一台作为NAT网关的主机访问公网，共享IP带宽。

**模拟场景**：假定目前存在VPC名为NAT01（10.1.0.0/16），下属两个子网：SNAT01(10.1.1.0/24)、SNAT02(10.1.2.0/24)，SNAT02下存在多台主机，实现子网SNAT02下的多台主机可通过子网SNAT01下一台作为NAT GW的主机上网。

**步骤一：在SNAT01子网下创建一台作为NAT网关的主机**

![image.png](https://img1.jcloudcs.com/cms/a39e84bd-e545-4bc6-b392-b282cc919f3420170921144239.png)

在SNAT01下创建一台主机，镜像选择CentOS-7.2 64位 NAT Gateway

![image.png](https://img1.jcloudcs.com/cms/c12f0c4b-92d1-40b1-b7b1-ad11a9e49ec620170921144253.png)

选择所属VPC为NAT01、子网为SNAT01

配置公网IP类型、带宽

主机命名为SNAT01

![image.png](https://img1.jcloudcs.com/cms/5b879ebe-a908-4997-ab3d-4b39e9c42afd20170921144319.png)

创建完成后，在主机列表页可以看到相同VPC下不同子网的主机情况

**步骤二：配置子网SNAT02****的路由表指向NAT****网关**

![image.png](https://img1.jcloudcs.com/cms/8a3d38ab-8b39-48e8-8da6-d17ec4a4df9220170921144330.png)

通过子网SNAT02查看和子网绑定的路由表

![image.png](https://img1.jcloudcs.com/cms/1d48dce1-083f-4881-9932-9c043203470b20170921144358.png)

编辑路由表：下一跳类型：云主机，下一跳主机：SANT01

配置完成后，子网SNAT02下的所有主机都可以通过SANT01作为NAT网关进行公网访问。

同理，可配置相同VPC下其他的子网路由。

**注意：如主机需要通过NAT****网关通信，不能选择与主机所在子网绑定同一张路由表的子网内的主机作为NAT****网关。**