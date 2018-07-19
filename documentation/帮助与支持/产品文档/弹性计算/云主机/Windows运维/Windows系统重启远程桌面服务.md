**Windows系统重启远程桌面服务**

Windows系统服务器默认远程登陆的3389端口暴露在公网，如果经常被暴力破解，即使不能成功入侵也会造成远程桌面服务异常；

建议修改远程桌面端口，也可以通过控制台终端登陆服务器重启远程桌面服务（Remote Desktop Services）的方式处理；

进入云主机控制台，点击页面的远程连接进入系统；

依次点击-开始-管理工具-服务，找到Remote Desktop Services右键点击重新启动即可；

![QQ截图20171121173136.png](https://img1.jcloudcs.com/cms/6bcd558b-2d58-4c58-b93e-f818359e4eca20171121173616.png)

重启后通过远程桌面测试登陆已经恢复；

![QQ截图20171121173448.png](https://img1.jcloudcs.com/cms/53a246d6-bac3-46d9-bf5a-b876ac4e671720171121173639.png)