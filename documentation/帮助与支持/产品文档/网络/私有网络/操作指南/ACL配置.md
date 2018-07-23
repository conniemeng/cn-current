# [转至元数据结尾](http://cf.jd.com/pages/viewpage.action?pageId=96004523#page-metadata-end)

[转至元数据起始](http://cf.jd.com/pages/viewpage.action?pageId=96004523#page-metadata-start)

# **ACL配置**

###

## **一、创建/删除网络ACL**

进入京东云控制台，点击左侧导航条 【私有网络 】— 【网络ACL】，进入网络ACL 页面

1、点击“创建”，弹出网络ACL创建弹框；

2、选择VPC，并输入网络ACL名称、描述，点击“确定”，即创建完成。请您注意在一个VPC创建的网络ACL只能适用于当前VPC，在其他VPC内不可使用。

3、删除网络ACL，点击要删除网络ACL对应操作框中的删除按钮，即可完成操作。

![图1.png](https://img1.jcloudcs.com/cms/30d07e63-b650-4fe6-8b84-ea1bf1ea4d8420170921152815.png)

![图2.png](https://img1.jcloudcs.com/cms/af30f4a1-0895-48df-8cb4-0c41ab447c3c20170921152822.png)

## **二、编辑网络ACL规则**

1、在网络ACL列表页面，点击要添加规则的网络ACL名称，进入到网络ACL详情页面；

2、根据需要添加的规则的类型，选择入站规则或出站规则选项卡：

3、点击“编辑规则”，设置协议类型、IP、端口以及策略后点击“确定”，即添加完成规则的修改。规则修改完成后及时生效 ；

![图3.png](https://img1.jcloudcs.com/cms/97ddecd1-4738-4a60-aa5d-7e6fd9d3eca620170921152829.png)

## **三、ACL关联子网**

1、在网络ACL列表页面，点击【关联子网】按钮；

2、在弹窗中选择需要绑定的子网，点击“确定”，即可将网络ACL规则绑定到子网，绑定完成后及时生效 ；

注意：一个网络ACL可以绑定多个子网、一个子网只能绑定一个网络ACL

![图5.png](https://img1.jcloudcs.com/cms/3e777c53-d887-465c-98a4-ed4a5b0afe4820170921152847.png)

### **四、ACL解关联子网**

1、在网络ACL列表页面，点击要添加规则的网络ACL名称，进入到网络ACL详情页面；

2、点击【关联子网】选项卡；

3、在关联子网列表中需要解关联的子网项后点击【解关联】按钮

4、在弹窗中点击"确定"