**SSH启动报错/var/empty/sshd must be owned by root and not group or world-writable**

**问题原因：**

/var/empty/sshd 目录权限异常导致，默认属主和属组是root账户。

**解决方法：**

手工修改目录属主和属组，执行

chown root.root /var/empty/sshd/

再次启动sshd服务，启动成功。如图：

![1.png](https://img1.jcloudcs.com/cms/fbc55624-ce33-41b1-82dc-a54944015c5d20180709114925.png)

如无法解决您的问题，请向我们提工单。