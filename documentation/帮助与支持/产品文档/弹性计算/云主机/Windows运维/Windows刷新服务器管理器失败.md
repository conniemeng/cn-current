**Windows刷新服务器管理器失败**

****

**问题现象:**

Windows 2008服务器管理器刷新失败，提示0x80070442错误，报错信息如下：

![image.png](https://img1.jcloudcs.com/cms/bbe88e76-2cd1-409d-ba20-a710a733d88520180131182652.png)

**问题原因：**

Windows Modules Installer服务器没有开启导致。

**解决方法：**

登录服务器桌面左下脚点击”开始”->”运行”，输入services.msc打开服务；

![image.png](https://img1.jcloudcs.com/cms/9243bfb6-7608-4ebb-a96a-ff4a0cc3d9b220180131182659.png)

找到Windows Modules Installer服务右键点击选择启动；

![image.png](https://img1.jcloudcs.com/cms/5dd2fc3d-a5b0-4185-9ca7-607ffda1c3d320180131182706.png)

之后再次打开服务器管理器便正常了。