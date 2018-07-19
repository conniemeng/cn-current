在安装有SQLServer数据库的云主机上，我们在使用数据库的过程中，有时候会在任务管理器里发现sqlservr.exe这个进程的内存和CPU占用率较高。

通过设置SQL Server服务器中的最大服务器内存，可以解决使用数据库时占用系统内存过高的问题。

1、远程登陆云主机进入SqlServer数据库，选中数据库实例，然后鼠标右键，点击属性

![091819v1b45mbkzi154bel.png](https://img1.jcloudcs.com/cms/b6e277ad-a1dd-442f-993c-619a489ee95620180131132806.png)

点击内存选项卡，默认最大服务器内存非常大，我们这里一般限制为云主机内存的50%，例如16G内存/*50%=8000MB.![091901i1cmyx5z1s5zajhm.png](https://img1.jcloudcs.com/cms/159064d4-b024-430f-930f-38cf5298249220180131133129.png)