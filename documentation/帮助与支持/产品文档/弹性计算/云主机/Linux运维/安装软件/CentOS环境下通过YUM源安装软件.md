# **CentOS环境下通过YUM源安装软件**

为了提升用户在云主机上的软件安装效率，减少下载和安装软件的成本，京东云提供了内网下载源。京东云会在每天00:00-02:00从mirrors.kernel.org对下载源进行同步。

在下载软件之前，您需要进行相关配置：

### **对于CentOS系统：**

1.备份mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup

2.下载新的CentOS-Base.repo 到/etc/yum.repos.d/

[](https://mirrors.jcloudcs.com/repo/CentOS-7.repo)

CentOS 5：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.jcloudcs.com/repo/CentOS-5.repo

CentOS 6：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.jcloudcs.com/repo/CentOS-6.repo

CentOS 7：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.jcloudcs.com/repo/CentOS-7.repo

3.运行yum makecache生成缓存

配置完成后即可根据需要下载安装软件。

****

**1. 安装步骤**

1) 登录操作系统为CentOS的云服务器后，默认已获取root权限。

注：严禁执行password命令，root密码默认不能被修改。

2) 在root权限下，通过以下命令来安装软件：
yum install [nginx][php][php-fpm][mariadb][mariadb-server][mysql][mysql-server]...

注：自CentOS 7来，MariaDB成为yum源中默认的数据库安装包，在CentOS 7以上的系统中使用yum安装MySQL包将无法使用MySQL。您可以选择使用完全兼容的MariaDB，或参考[这里](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)进行MySQL较低版本的安装。

3) 系统会自动搜索相关的软件包和依赖关系，并且在界面中提示用户确认搜索到的软件包是否合适，如下图所示：![](https://img1.jcloudcs.com/cms/03fffb64-3bd9-4ab0-b207-0ff54d197e6920170324203811.png)

4) 输入“y”确认后，开始安装软件，安装完成后会提示“Complete”，如下图所示：

![](https://img1.jcloudcs.com/cms/52ba93cb-6993-4dde-9e64-431237590c0120170324203829.png)

**2. 查看安装的软件信息**

软件安装完成后，可通过以下命令查看软件包具体的安装目录。
rpm -ql nginx

以查看刚刚安装成功的nginx的安装目录为例：

![](https://img1.jcloudcs.com/cms/a177b184-c5ba-41bf-9648-0b923963277120170324203845.png)

可通过以下命令查看软件包的版本信息。
rpm -q nginx

以查看nginx的版本为例

![](https://img1.jcloudcs.com/cms/58cd4030-6607-4f74-b9e8-89515ae04b1220170324203854.png)