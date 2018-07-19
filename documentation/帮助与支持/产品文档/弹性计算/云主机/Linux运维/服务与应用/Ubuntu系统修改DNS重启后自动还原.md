**Ubuntu系统修改DNS重启后自动还原的处理方法**

**问题现象：**

ubuntu系统的云主机，修改 resolv.conf 文件中的DNS信息，重启云主机后， resolv.conf 文件中的信息会还原为修改前的信息；

**问题原因：**

ubuntu 系统中 /etc/resolv.conf 其实是一个软连接，如下图，文件软连到 /run/resolvconf/resolv.conf；

![1.png](https://img1.jcloudcs.com/cms/a3119791-2efd-4093-87b8-f50f847b7fa620180709145524.png)

**解决方法：**

可以直接修改/run/resolvconf/resolv.conf文件中的DNS信息；

![2.png](https://img1.jcloudcs.com/cms/7bf83fc7-11e1-4c50-8ff7-70481e0f424c20180709145607.png)

如无法解决您的问题，请向我们提工单。