**Linux系统tail查看日志提示空间不足**

**问题现象：**

Linux主机 tail 查看日志时，提示空间不足，具体报错信息类似如下：

![1.png](https://img1.jcloudcs.com/cms/186b1315-7830-442e-a320-26c5821e8e4620171025143415.png)

**问题原因：**

tail 操作需要系统监控配额。同一用户同时添加的 watch 数目超出了内核 max_user_watches 参数配置，导致了该问题。

**处理办法：**

修改 /proc/sys/fs/inotify/max_user_watches 为较大值：

sudo sysctl fs.inotify.max_user_watches=8192 /# 以8192为例，此方式临时生效

如果想永久生效，需要修改/etc/sysctl.conf，添加 max_user_watches=8192，然后通过如下指令生效：

sysctl -p

如无法解决您的问题，请向我们提工单。