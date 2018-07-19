**Windows文件属性没有安全选项卡**

**问题现象：**

Windows服务器鼠标右键点击文件或者文件夹属性的时候，没有安全选项卡，导致无法修改文件或者文件夹的权限，现象如图：

![1.png](https://img1.jcloudcs.com/cms/0a058147-88d2-4b4c-88c3-a70f5918d99520170907112652.png)

**解决办法：**

1.点击开始-运行-输入gpedit.msc打开组策略。

![2.png](https://img1.jcloudcs.com/cms/6deef7db-8707-4460-969e-74c5c90ebd4420170907112740.png)

2.点击用户配置-管理模版-Windows组件-Windows资源管理器-右侧找到"删除"安全"选项卡"。

![3.png](https://img1.jcloudcs.com/cms/09d25c23-bf15-44bb-9d4b-3dd2ad624eda20170907112801.png)

3.双击打开"删除"安全"选项卡"，改为"未配置"，点击确定即可。之后右键点击文件或者文件夹便可以看到安全选项卡了。

![4.png](https://img1.jcloudcs.com/cms/335cdd47-150f-48d7-880e-84e762b3e45620170907112922.png)

![5.png](https://img1.jcloudcs.com/cms/26c5b56f-07c4-45ae-8622-672a79945af720170907113051.png)

如无法解决您的问题，请向我们提工单。