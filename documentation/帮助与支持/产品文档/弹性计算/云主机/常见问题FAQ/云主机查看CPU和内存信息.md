# 云主机查看CPU和内存信息

### Windows系统云主机查看CPU和内存信息：

在桌面任务栏鼠标右键点击，选择弹出菜单里的任务管理器选项启动任务管理器，然后选择性能标签页，看到红框处的内存大小即为云主机的总内存大小，如图所示：

![WIN_INFO2.JPG](https://img1.jcloudcs.com/cms/a19d5fb4-7511-4d3a-9e58-3d97b0528d8a20180122145908.JPG)

再点击左下角红框处的打开资源监视器按钮启动资源监视器，选择CPU标签页，在右侧红框处可以看到CPU0、CPU1等多个性能监视窗口，如图所示。云主机的CPU配置是几核，此处就会有几个CPU窗口。例如云主机CPU是4核，则此处显示CPU0、CPU1、CPU2、CPU3四个窗口。

![WIN_INFO3.JPG](https://img1.jcloudcs.com/cms/1b5fb95f-9c2a-4a44-96aa-4d465e85254120180122150150.JPG)

### Linux系统云主机查看CPU和内存信息：

执行命令lscpu|grep "CPU(s):"查看CPU核心数，如图所示：

![cpu_linux2.JPG](https://img1.jcloudcs.com/cms/262c3737-9819-4b71-a3d6-2c5e8e20392020180122151737.JPG)

另外CPU核心数也可以通过cat /proc/cpuinfo|grep processor看到的CPU个数确认，如果是4核CPU，则可以看到processor0到processor3共计4个CPU信息，还可以通过top命令按1看到不同CPU核心的信息，如图所示：

![cpu_linux1.JPG](https://img1.jcloudcs.com/cms/1a85e484-af67-439b-a0d3-b9e55d74cf4c20180122151642.JPG)

执行命令cat /proc/meminfo|grep MemTotal查看云主机内存信息，单位为KB，如图所示：

![mem_linux1.JPG](https://img1.jcloudcs.com/cms/1d22a6f3-2f04-4747-992d-e770f8cd876220180122152118.JPG)