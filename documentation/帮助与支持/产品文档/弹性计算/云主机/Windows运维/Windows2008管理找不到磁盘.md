**Windows2008计算机管理找不到磁盘管理的处理方法**

**问题现象：**

Windows 2008服务器在计算机管理的存储里面，查看不到磁盘管理，无法对磁盘做管理。

![1.png](https://img1.jcloudcs.com/cms/a11df6ca-698c-477c-bdfd-1b71203707e620170829155934.png)

**问题原因：**

一般都是系统组策略中的磁盘管理服务被禁用导致的

**解决办法：**********

1.点击开始-运行-输入gpedit.msc，打开组策略。

![2.png](https://img1.jcloudcs.com/cms/36191137-7d5f-4147-bb55-1b880644e1dc20170829160143.png)

2.依次点击【本地计算机策略】→【用户配置】→【管理模板】→【Windows组件】→【Microsoft 管理控制台】→【受限的/许可的管理单元】→双击【磁盘管理】。

![3.png](https://img1.jcloudcs.com/cms/12a31751-f699-4acf-ac51-500b9b1ecbf420170829160216.png)

3.点击【未配置】→【确定】。

![4.png](https://img1.jcloudcs.com/cms/066ccbac-7aa1-4cba-87d8-f9281f7bcb6320170829160231.png)

4.打开命令提示符，执行gpupdate 更新组策略。

![5.png](https://img1.jcloudcs.com/cms/73daad95-99dd-4ebe-b24c-ee9f578ebb5020170829160332.png)

如无法解决您的问题，请向我们提工单。