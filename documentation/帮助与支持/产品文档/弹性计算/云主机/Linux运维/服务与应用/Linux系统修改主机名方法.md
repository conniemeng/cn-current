**Linux系统修改主机名方法**

修改Linux系统主机名常见的有两种方式，本文对此进行概要说明。

**临时生效修改**

使用命令行修改 hostname 主机名(可自定义)，重新登录 shell 生效。

![1.png](https://img1.jcloudcs.com/cms/282e5ae8-41e5-457e-aa7f-7c84e1cb5aaa20170808112615.png)

重新登录 shell 后可以看到已经生效

![2.png](https://img1.jcloudcs.com/cms/00549eb3-ed08-4d52-9a77-d85d8873efe120170808112648.png)

**永久生效修改**

以 CentOS 系统为例，需要更改配置文件生效，修改 /etc/sysconfig/network 里的 HOSTNAME=主机名(可自定义)，重启生效。

![3.png](https://img1.jcloudcs.com/cms/a145f69e-b99c-49bf-b044-a58f280eab3620170808112742.png)

![4.png](https://img1.jcloudcs.com/cms/01c4cf7a-49c5-40b7-aab4-dbb410c00eba20170808112826.png)

如果是 Ubuntu 系统，则需要修改文件 /etc/hostname， 将其对应的主机名修改为新的主机名。

最后，需要将 /etc/hosts 中 127.0.0.1 对应的老主机名更换为新的主机名。

![6.png](https://img1.jcloudcs.com/cms/ad8b3ad8-2b5c-4580-ae90-7c6859b6f80020170808113007.png)

![5.png](https://img1.jcloudcs.com/cms/d79dd5b1-938c-49ac-a196-87baf1aff10020170808112922.png)

注意：如果是 CentOS 7 操作系统，可以使用命令 hostnamectl set-hostname 主机名来修改，修改完毕后重新 SHELL 登录即可。

![7.png](https://img1.jcloudcs.com/cms/a4857dca-5169-429f-88c0-47a8e0729f7720170808113106.png)

如无法解决您的问题，请向我们提工单。