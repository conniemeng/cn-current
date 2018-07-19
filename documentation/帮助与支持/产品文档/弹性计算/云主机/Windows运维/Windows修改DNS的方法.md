**问题描述：**

Windows系统如何修改DNS。

**解决方案：**

Windows系统服务器，DNS默认是自动获取的，如果用户想使用自己配置的DNS或者公网的dDNS进行解析，可以参考如下方法修改下服务器的DNS：

1.打开网络和共享中心；

![image.png](https://img1.jcloudcs.com/cms/8b218168-c127-4dee-a4bf-3635ff8f19ce20180202153514.png)

2.选择"更改适配器设置"；

![image.png](https://img1.jcloudcs.com/cms/660199c4-69aa-4fb2-a2ef-08a77709479c20180202153522.png)

3.选择网卡，右击选择“属性”；

![image.png](https://img1.jcloudcs.com/cms/570ede50-35db-487d-9c47-9d9044dd282620180202153532.png)

4.双击“Intrtnet协议版本4（TCP/IPV4）”，在出现的选项卡下方向输入要使用的DNS地址就可以，可以使用公网114.114.114.114和114.114.115.115这组DNS，或者改为其他您想使用公网DNS。

![image.png](https://img1.jcloudcs.com/cms/3aa6deac-c571-4e8c-aa13-e2f05e94f96e20180202153632.png)