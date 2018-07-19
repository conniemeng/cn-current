**Windows系统**

### sc命令

sc命令是Windows原生的服务控制命令，通过它可以方便地添加、删除标准的Windows服务程序：

/# 添加服务

sc create ServiceName binpath= "D:\services\xxx.exe"

/# 移除服务

sc delete ServiceName

请注意:

* 
binpath参数后面必须有一个空格
* 
添加完服务后，需要自行配置一下，如将启动类型设置为“自动”
* 
用户可以通过services.msc查看、管理已注册的服务

****

### **添加自启动服务例子**

（1）在管理员权限下打开cmd，执行如下指令，将wosigncode.exe应用程序设置为服务程序

sc create myservice binpath= "c:\wosigncode.exe"

执行成功后见下图：

![](https://img1.jcloudcs.com/cms/728b2519-dbe9-4af1-8ad8-f3cd61eba7e220170512185658.png)

（2）运行-> 输入services.msc

### ![](http://img1.jcloudcs.com/cms/4852e269-ba37-4057-8d17-472bf3255bf920170512185717.png)

（3）找到刚才添加的服务myservice，单击右键，选择“属性”（见下图）

![](https://img1.jcloudcs.com/cms/c0c1335d-529f-4db3-a234-ea72e9cc777220170512185759.png)

（4）在启动类型中，选择“自动”，然后单击“启动”，最后单击“确定”即可完成该程序开机自启动设置。

### ![](http://img1.jcloudcs.com/cms/142c0722-4861-4f1d-987a-2631f618e66c20170512185817.png)