**SSH登录报Disconnected:No supported authentication methods available**

注意：本文相关 Linux 配置及说明已在 CentOS 6.5 64 位操作系统中进行过测试。其它类型及版本操作系统配置可能有所差异，具体情况请参阅相应操作系统官方文档。

**问题现象**

当您通过 SSH 客户端Linux 云主机时，输入正确的账号密码，也会出现类似如下错误信息。

![1.png](https://img1.jcloudcs.com/cms/1c53f7c5-edc1-4a5a-ab64-9d3bf3cebd3c20171120141025.png)

• Permission denied (publickey,gssapi-keyex,gssapi-with-mic).

• sshd[10826]: Connection closed by XX.XX.XX.XX.

• Disconnected: No supported authentication methods available.

**问题原因**

参数 PasswordAuthentication 的默认值为 yes，SSH 服务将其值置为 no 以禁用密码验证登录，导致此类故障。需要修改 PasswordAuthentication 配置解决此问题。

**解决方法**

建议在修改配置文件之前先创建系统盘镜像备份。

1.通过 VNC 连接并登录到 Linux 云主机。

2.执行命令，查看 SSH 服务配置，并注意是否包含类似如下配置：

cat /etc/ssh/sshd_config

![2.png](https://img1.jcloudcs.com/cms/56b14cf3-3315-4e37-8922-7c6d7be06d1620171120141335.png)

3.执行命令。

vi /etc/ssh/sshd_config

按下 i 编辑 SSH 服务配置文件，将参数 PasswordAuthentication 设置为 yes，或者在 PasswordAuthentication 参数前添加井号（/#），按下 Esc 退出编辑模式，并输入 :wq 保存退出。

![3.png](https://img1.jcloudcs.com/cms/e000e8f5-9334-4829-b6ed-0d0c9c83902a20171120141527.png)

4.执行命令， 重启 SSH 服务。

service sshd restart

5.在控制台重启 Linux 实例。

6.使用 SSH 客户端重新登录 Linux 云主机。

如无法解决您的问题，请向我们提工单。