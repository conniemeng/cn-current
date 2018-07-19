**Windows自动更新消耗cpu内存过高**

**问题现象**

Windows默认如果开启了自动更新功能，会造成内存使用率过高或者CPU升高的情况。体现在svchost.exe这个进程占用内存很多，CPU有时候也会升高。

![1.png](https://img1.jcloudcs.com/cms/a4130be9-c37f-4df7-b1f4-c9cd7530020b20170817110312.png)

**问题原因**

此进程消耗服务器资源主要有两种可能：

1、服务器被黑了存在木马病毒。

2、因为Windows自动更新功能没有关闭。如果服务器中没有异常木马病毒存在，通过关闭Windows Update功能即可解决。

**解决办法**

1.安装安全杀毒软件，进行查杀病毒。

2.禁用windows update自动更新。运行中输入gpedit.msc，在计算机配置，管理模板，windows update，配置自动更新，选择已禁用。

![3.png](https://img1.jcloudcs.com/cms/1d94ad50-eece-4fe5-b9b0-4b71efcc187320170817111307.png)

![2.png](https://img1.jcloudcs.com/cms/df312561-2325-4bbc-bce4-a9438741e87820170817111344.png)

如无法解决您的问题，请向我们提工单。