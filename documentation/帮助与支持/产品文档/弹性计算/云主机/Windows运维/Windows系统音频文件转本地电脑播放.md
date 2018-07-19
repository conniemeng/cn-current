**Windows系统音频文件转本地电脑播放**

**问题现象：**

windows系统远程连接后，右下角的声音显示红叉，无法播放远程声音；

![1.png](https://img1.jcloudcs.com/cms/4d978a88-c168-47a2-bd43-305ee4dadea020180417161628.png)

**处理方法：**

可以通过设置本地电脑远程桌面工具的方法，将远程的声音在本地电脑上播放；
云主机内请先调整下如下设置；

**windows 2008系统：**1 远程连接后，点击开始-管理工具-远程桌面服务-远程桌面会话主机；

![2.png](https://img1.jcloudcs.com/cms/c763cbe1-e189-4982-a2d0-e7183cc8bec120180417161656.png)

2 双击rdp-tcp，选择客户端设置，将音频和视频播放的勾选取消；

![3.png](https://img1.jcloudcs.com/cms/bd19f9db-2ba5-4928-b56a-58143e2c2fde20180417161720.png)

3 点击开始-运行-输入services.msc，找到“Windows Audio”服务，将此服务设置为自动，并启动下，之后将此次的远程连接关闭；

![4.png](https://img1.jcloudcs.com/cms/4c73d9bb-d25a-4023-a698-ddced48e573620180417161749.png)

**windows 2012系统：**

1 打开windows powershell，输入gpedit.msc，打开组策略；

![5.png](https://img1.jcloudcs.com/cms/87bfa062-10c0-4b31-b5d0-55a1782ae30f20180417161957.png)

![6.png](https://img1.jcloudcs.com/cms/8e369579-9f8c-40e2-b14b-c52ae83cdaa620180417162012.png)

2 依次点击“计算机配置”-“管理模版”-“windows 组件”-“远程桌面服务”-“远程桌面会话主机”-“设备和资源重定向”，打开“允许音频和视频播放重定向”，选择“已启用”;

![7.png](https://img1.jcloudcs.com/cms/76d23947-90b5-4133-8e1a-962a9dfebe3820180417162153.png)

3 继续在windows powershell中输入services.msc打开服务，找到“Windows Audio”服务，将此服务设置为自动，并启动下，之后将此次的远程连接关闭；

![8.png](https://img1.jcloudcs.com/cms/13d61767-1ae6-46eb-8f68-0ebb8240c8a120180417162215.png)

以上配置调整完成后，打开本地远程桌面软件进行配置。

**本地电脑Windows xp系统：**

打开本地远程桌面软件，点击 选项 - 本地资源，选择远程计算机声音的下拉菜单，选择 带到这台计算机。

![9.png](https://img1.jcloudcs.com/cms/a6092cec-0028-4ba2-b976-84fb9a15e85b20180417162513.png)

****

**本地电脑Windows 7系统：**

打开本地远程桌面软件，点击“选项”-“本地资源”，在远程声音处点击“设置”，弹出的选项卡中的远程音频播放处，选择“在此计算机中播放”，点击确定；

![2.png](https://img1.jcloudcs.com/cms/abdc5966-923b-4c71-ab64-d73c56c320bc20171211111033.png)

![3.png](https://img1.jcloudcs.com/cms/ecae75df-ff53-44d2-8e1d-7ade6d684cdb20171211111159.png)

再次连接后，可以看到右下角声音处显示已经正常，此时在远程打开音频文件，本地是可以正常听到声音的；

![10.png](https://img1.jcloudcs.com/cms/f061f4d9-b7bc-4590-9289-2b8c33d2da1120180417162743.png)

如无法解决您的问题，请向我们提工单。