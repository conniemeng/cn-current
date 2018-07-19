**Windows系统设置不锁屏**

以windows2012系统为例，通过控制台，远程连接vnc连接云主机，第一次登录需要输入ctrl+alt+delete进入系统。断开vnc，如果一段时间不登录，再次登录vnc后还是会提示让输入ctrl+alt+delete。可以尝试通过以下方式设置系统不锁屏。

1.左下角开始，选择运行。

![1.png](https://img1.jcloudcs.com/cms/8ecf75c0-9a18-455b-89b3-7037ac3631c620180201230201.png)

2.输入gpedit.msc，进入组策略配置界面。

![2.png](https://img1.jcloudcs.com/cms/30f99901-25b3-42d8-8e89-dc4e1687caf520180201230255.png)

3.选择计算机配置--管理模版--控制面板--个性化，右侧选择不显示锁屏。

![3.png](https://img1.jcloudcs.com/cms/4137e146-bd39-4e40-9737-e7ae4c90ce0120180201230345.png)

4.选择已启用，应用。

![4.png](https://img1.jcloudcs.com/cms/2fc960bc-114a-445b-ad5e-3c2a295463bd20180201230446.png)

这样在退出vnc，再次连接vnc登录时就不会进入锁屏界面了。

如无法解决您的问题，请向我们提工单。