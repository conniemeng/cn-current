**Windows2008服务器管理器刷新报0x80070422错误**

**问题现象：**

windows服务器管理器刷新失败，提示如下错误：

![1.png](https://img1.jcloudcs.com/cms/bbd803a4-7e84-4fce-a611-ac2230f27f6520180709113059.png)

**问题原因：**

Windows Modules Installer服务器没有开启导致。

**解决方法：**

登录服务器桌面左下脚点击”开始”->”运行”，输入services.msc打开服务；

![2.png](https://img1.jcloudcs.com/cms/3090bea4-53c2-437d-86a7-decc4e0b22b420180709113339.png)

找到Windows Modules Installer服务右键点击选择启动；

![3.png](https://img1.jcloudcs.com/cms/cdad4327-c338-47a3-8d2b-b77b103170b720180709113416.png)

之后再次打开服务器管理器便正常了。

如无法解决您的问题，请向我们提工单。