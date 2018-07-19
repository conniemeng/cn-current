**iis7.5设置日志时间和本地时间同步**

**问题现象：**

iis服务中的web日志和ftp日志记录的时间点和服务器系统时间不一致，相差8小时，如图：

![1.png](https://img1.jcloudcs.com/cms/b7994f3d-eafd-4bb9-9bc6-6f55505f770720171123162621.png)

**问题原因：**

由于IIS日志的机制，IIS日志W3C格式是以格林尼治时间创建的，因此和服务器系统时间要差8个小时。

**解决办法：**

打开iis管理器，点击ftp站点，右侧点击ftp日志。

![2.png](https://img1.jcloudcs.com/cms/c6f9b778-95af-49da-ae7c-6b443b829e9f20171123162956.png)

将最下面的使用本地时间进行文件命名和滚动更新选项前面打钩，点击应用即可。

![3.png](https://img1.jcloudcs.com/cms/7551db2a-40eb-48df-bae3-ff1f2da5b36820171123163024.png)

如无法解决您的问题，请向我们提工单。