**Windows系统svchost.exe进程占用cpu，内存资源高的处理办法**

**问题描述**

Windows系统内名为【svchost.exe】的进程，CPU或内存资源使用率一直居高不下，导致系统卡顿，影响正常使用。什么是 svchost.exe，svchost.exe 是计算机上的一个进程，该进程是Windows上用于执行各种功能的其它单独服务的宿主。可以有多个svchost.exe 的实例在计算机上运行，其中每个实例都包含不同的服务。svchost.exe 的一个实例可能有单个服务或多个服务。

**定位及解决办法**

使用任务管理器做简要分析，打开系统自带的【任务管理器】，快速判断出相应svchost进程下挂载的对应服务：

1.通过右键单击任务栏，然后单击“启动任务管理器”，打开“任务管理器”。

2.切换到“进程”选项卡。

3.单击“显示所有用户的进程”，若系统提示您输入管理员密码或进行确认，请键入该密码或提供确认。

4.右键单击资源使用过高的 svchost.exe实例，然后单击“转到服务”按钮，与进程关联的服务将在“服务”选项卡上突出显示。

![2.png](https://img1.jcloudcs.com/cms/09955222-c9f9-44b6-ba68-5daaf65c65bd20170821102733.png)

![3.png](https://img1.jcloudcs.com/cms/28a2eb9b-c6cb-4d15-a319-bd6fa5bc940920170821102808.png)

使用SC Config命令隔离服务

在找到CPU占用高的Svchost之后，也可以尝试通过SC Config命令将svchost中驻存的服务“独立”出来到单独的svchost中运行：

1.客户遇到高CPU的情况，定位下来发现是svchost占用CPU较高。通过tasklist命令发现对应的svchost进程中有多个服务驻存。命令提示符下执行：tasklist /svc

![1.png](https://img1.jcloudcs.com/cms/de2c1fa1-2ea5-4bae-9336-58d5e78fd1b320170821103230.png)

2.通过Sc config 命令我们可以将这些服务独立出来运行到单独的svchost进程中，例如：wuauserv（Windows Update服务）。命令提示符下执行：

sc config wuauserv type= own

![4.png](https://img1.jcloudcs.com/cms/4ce2b961-f9a4-40ae-a529-ac0678f7e33320170821103511.png)

执行成功后重启服务器, 执行命令tasklist /svc | findstr /I /C:wuau，发现Windows Update服务已经成功独立。

![6.png](https://img1.jcloudcs.com/cms/641ae61e-17ca-4e96-8a94-feed8977b88620170821103619.png)

3.经过监控发现确实是Windows Update的服务消耗CPU较高，后续响应的调整Windows Update策略晚上进行更新，避免工作时间影响服务器业务的运行。

![5.png](https://img1.jcloudcs.com/cms/823db9bb-eea0-4056-899d-705f0fe88dd220170821104028.png)

如果恢复该服务与其它服务一起驻存到相同svchost中，请执行如下命令sc config wuauserv type= share，重启服务器生效。

![7.png](https://img1.jcloudcs.com/cms/63c55ea3-5813-43c4-8cfb-35de37e2745220170821104358.png)

如无法解决您的问题，请向我们提工单。