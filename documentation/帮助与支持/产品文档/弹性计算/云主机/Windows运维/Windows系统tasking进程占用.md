**Windows系统tasking.exe进程占用大量cpu资源**

**问题现象：**

任务管理器中查看tasking.exe进程占用大量cpu资源，结束进程树后会自动再开启，删除文件也没有用。如图：

![2.png](https://img1.jcloudcs.com/cms/2e119757-058f-413f-8bb4-a8bb84962bb420171031145341.png)

**问题原因：**

National Instruments Domain Service启动运行形成的进程导致。

**解决办法：**

首先是在搜索里打开msconfig，常规设置里改成有选择的启动，点进服务，先点一下左下角隐藏Microsoft服务，从剩下的服务中找到名为National Instruments Domain Service的一条，把它前面的勾去掉然后应用，重启服务器生效。如图：

![1.png](https://img1.jcloudcs.com/cms/00cf8907-19c1-46d8-86bf-37d64f41e15b20171031145628.png)

如无法解决您的问题，请向我们提工单。