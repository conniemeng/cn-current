**BDOS版本**

此版本主要介绍Web界面登录的方式。

步骤1根据web访问的提示信息，将您的公网IP和域名（例如：114.67.248.172 bdos.jcloud.com）粘贴到C:\Windows\System32\drivers\etc下hosts文件中。

备注：公网IP即为，“集群详情”页面-“硬件信息”中Master1节点的外网IP。

步骤 2 由于此域名符合HTTP协议，端口为80。因此需要打通80端口的入站策略。设置时注意要选择对应的地域，以免设置后不生效。

设置方式：网络ACL在“网络-私有网络-网络ACL”页面，选择入站规则，编辑-添加新规则，编辑完点击保存。见下图。

![图片.png](https://img1.jcloudcs.com/cms/6b43d849-60dc-46fa-b3db-dfce942d4da320180412155745.png)

步骤3 打开浏览器，输入bdos.jcloud.com

步骤4 成功显示登录页面。

初始帐号 superadmin ，初始密码 jupiter123。

![图片.png](https://img1.jcloudcs.com/cms/f4e93b82-a603-4411-ba08-69eefb769f1420180412155808.png)