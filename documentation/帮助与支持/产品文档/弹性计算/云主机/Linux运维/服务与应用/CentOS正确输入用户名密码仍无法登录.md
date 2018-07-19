# CentOS正确输入用户名仍无法登录

有时在登录CentOS云主机时会遇到正确输入用户名和密码之后，无法登录系统，自动跳转回输入用户名和密码界面，再次输入后仍不能登录，如此反复循环。如图一和图二所示：

![](https://img1.jcloudcs.com/cms/8cd5096c-3445-4ca0-a756-fade6539b96620171225141331.JPG)

![](https://img1.jcloudcs.com/cms/9ccadba3-bb7f-432c-8249-37ef9419649620171225141331.JPG)

这种情况一般是/etc/pam.d/login文件中缺少session required/lib64/security/pam_limits.so内容或者该内容存在但pam_limits.so文件的路径不正确导致（有问题的路径为/lib/security/pam_limits.so或pam_limits.so，如图三和图四所示）需要进入单用户模式进行修改。

![](http://img1.jcloudcs.com/cms/a4b6025f-dcf4-4948-a569-4080cf9638a820171225141331.JPG)

![](http://img1.jcloudcs.com/cms/f558e12d-38e7-49cd-a7a8-cc8b2c87af9920171225141331.JPG)

在远程连接VNC页面点击右上角Send CtrlAltDel重启云主机，按照文档（[http://opms.jcloud.com/archives/220](http://opms.jcloud.com/archives/220)）给出的方法进入单用户模式。
执行命令 vi /etc/pam.d/login编辑login文件。
查找文件最后一行是否有session required/lib64/security/pam_limits.so内容且未被注释（行首没有/#则未被注释），如果没有该行，则按i进入insert模式添加该内容。
如果有session required/lib/security/pam_limits.so或session requiredpam_limits.so内容，则将其修改为session required/lib64/security/pam_limits.so。
修改完毕后wq保存文件并退出vi，如图五所示：

![](http://img1.jcloudcs.com/cms/2d3562c2-8829-460c-a0ce-0d1a63cf347e20171225141331.JPG)

在单用户模式输入reboot重启云主机，如图六所示：

![](http://img1.jcloudcs.com/cms/dd8cf163-4eb3-439f-b91b-c02c25f4e71e20171225141331.JPG)

重新启动后，正确输入用户名密码可以登录系统。