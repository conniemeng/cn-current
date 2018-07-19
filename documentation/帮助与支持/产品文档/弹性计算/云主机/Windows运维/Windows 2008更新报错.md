**Windows2008 更新补丁报“8000FFFFwindows update 遇到未知错误”**

**问题现象：**

Windows2008 R2 更新补丁报“代码 8000FFFF windows update 遇到未知错误“：

![1.png](https://img1.jcloudcs.com/cms/a80d4e95-eb3e-4283-86e6-83a8eaf4134520170828140220.png)

**问题原因：**

该问题主要原因是因为 C 盘无 user 权限，导致更新的补丁无法正常安装。

**解决办法：**

为C盘加上user权限，只需要给读写权限即可，为了系统安全在补丁更新完成以后去掉user权限，避免留下安全隐患。

![2.png](https://img1.jcloudcs.com/cms/8b378173-73c6-4d95-b6f2-9c67d458150320170828143933.png)

![3.png](https://img1.jcloudcs.com/cms/daca6a51-5d95-48b4-af90-2d9cf006366220170828143952.png)

如果以上方法还是无法解决，参考以下方法，通常可以解决：

1.停止自动更新 和 BITS服务。在命令提示符中执行：

net stop wuauservnet stop bits

***![4.png](https://img1.jcloudcs.com/cms/b7824aae-723f-4733-bb63-9f4ea35a655d20170828144148.png)***

2.删除系统中 “C:\Windows\SoftwareDistribution” 文件夹。

3.启动自动更新服务和 BITS服务，当这两个服务运行后会自动创建“C:\Windows\SoftwareDistribution”文件夹。在命令提示符中执行：

net start wuauservnet start bits

![5.png](https://img1.jcloudcs.com/cms/2fe923c7-7896-4314-8047-02ffc5abd23620170828144844.png)

4.停止 Cryptographic服务。在命令提示符中执行：

net stop cryptsvc

![6.png](https://img1.jcloudcs.com/cms/c2694f95-0567-4ec5-a1b3-c639289ea10d20170828145211.png)

5.重命名 C:\windows\System32\catroot2文件夹为：C:\windows\System32\catroot2.bak。

6.C:\Windows\SoftwareDistribution” 文件夹生成后, 做自动更新检测，在命令提示符中执行：

wuauclt.exe /resetauthorization /detectnow

![7.png](https://img1.jcloudcs.com/cms/d5784266-4d80-48e6-b3ca-47f5b7c0ae1620170828145603.png)

7. 15分钟后查看系统是否检测到更新，如果检测到，通常就可以正常安装。

如无法解决您的问题，请向我们提工单。