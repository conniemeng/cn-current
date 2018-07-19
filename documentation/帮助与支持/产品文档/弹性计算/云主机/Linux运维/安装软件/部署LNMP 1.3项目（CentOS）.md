**部署LNMP 1.3项目（CentOS）**

**系统需求:**

CentOS/RHEL/Fedora/Debian/Ubuntu/Raspbian Linux系统

需要5GB以上硬盘剩余空间

需要128MB以上内存(如果为128MB的小内存VPS,Xen的需要有SWAP,OpenVZ的至少要有128MB以上的vSWAP或突发内存)，注意小内存请勿使用64位系统！

安装MySQL 5.6或5.7及MariaDB 10必须1G以上内存!。

VPS或服务器必须已经联网，且必须设置的是网络源不能是光盘源，同时VPS/服务器 DNS要正常！

Linux下区分大小写，输入命令时请注意！

CentOS 5,Debian 6及之前版本其官网已经结束支持无法使用！

LNMP一键安装包 V1.3 已经在京东云等众多VPS的CentOS 6-7、RHEL 6-7、Ubuntu 14.04-16.04的32位和64位系统上测试通过(CentOS 5,Debian 6及之前版本其官网已经结束支持无法使用)。

**安装步骤:**

**1、使用putty或类似的SSH工具登陆VPS或服务器：**

登陆后运行：screen -S lnmp

如果提示screen: command not found 命令不存在可以执行：yum install screen 或 apt-get install screen安装，详细内容参考screen教程。

**2、下载并安装LNMP一键安装包：**

您可以选择使用下载版(推荐美国及海外VPS或空间较小用户使用)或者完整版(推荐国内VPS使用，国内用户可用在下载中找国内下载地址替换)，两者没什么区别，只是完整版把一些需要的源码文件预先放到安装包里。

安装LNMP稳定版

wget -c http://soft.vpser.net/lnmp/lnmp1.3-full.tar.gz && tar zxf lnmp1.3-full.tar.gz && cd lnmp1.3-full && ./install.sh lnmp

安装LNMP测试版

wget -c http://soft.vpser.net/lnmp/lnmp1.4beta.tar.gz && tar zxf lnmp1.4beta.tar.gz && cd lnmp1.4 && ./install.sh lnmp

[root@lnmp-software ~]/# yum update -y

[root@lnmp-software ~]/# tar xvf lnmp1.3-full.tar.gz

[root@lnmp-software ~]/# cd lnmp1.3-full

[root@lnmp-software lnmp1.3-full]/# ls

ChangeLog conf include init.d install.sh License lnmp.conf php5.2.17.sh pureftpd.sh readme src uninstall.sh upgrade.sh

[root@lnmp-software lnmp1.3-full]/# ./install.sh

默认安装lnmp可不写，如需要安装LNMPA或LAMP，将./install.sh 后面的参数替换为lnmpa或lamp即可。如需更改网站和数据库目录先修改 lnmp.conf 文件。

如下载速度慢请更换其他下载节点，详情请看下载页面。LNMP下载节点具体替换方法。

按上述命令执行后，会出现如下提示：

![https://lnmp.org/images/1.3/lnmp-1.3-install-1.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-1-png.png)

需要设置MySQL的root密码（不输入直接回车将会设置为root）如果输入有错误需要删除时，可以按住Ctrl再按Backspace键进行删除。输入后回车进入下一步，如下图所示：

![https://lnmp.org/images/1.3/lnmp-1.3-install-2.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-2-png.png)

询问是否需要启用MySQL InnoDB，InnoDB引擎默认为开启，一般建议开启，直接回车或输入 y ，如果确定确实不需要该引擎可以输入 n，输入完成，回车进入下一步

选择MySQL版本，目前提供了较多版本的MySQL和MariaDB，需要注意的是MySQL 5.6,5.7及MariaDB 10必须在1G以上内存的更高配置上才能选择：

![https://lnmp.org/images/1.3/lnmp-1.3-install-3.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-3-png.png)

输入对应MySQL或MariaDB版本前面的序号，回车进入下一步，选择PHP版本：

注意：选择PHP7等高版本时需要自行确认是否与自己的程序兼容。

![https://lnmp.org/images/1.3/lnmp-1.3-install-4.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-4-png.png)

输入要选择的PHP版本的序号，回车进入下一步，选择是否安装内存优化：

![https://lnmp.org/images/1.3/lnmp-1.3-install-5.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-5-png.png)

可以选择不安装、Jemalloc或TCmalloc，输入对应序号回车，直接回车为默认为不安装。

如果是LNMPA或LAMP的话还会提示“Please enter Administrator Email Address:”，需要设置管理员邮箱，该邮箱会在报错时显示在错误页面上。

![https://lnmp.org/images/1.3/lnmp-1.3-install-6.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-6-png.png)

再选择Apache版本

![https://lnmp.org/images/1.3/lnmp-1.3-install-7.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-7-png.png)

按提示输入对应版本前面的数字序号，回车。

提示”Press any key to install…or Press Ctrl+c to cancel”后，按回车键确认开始安装。

LNMP脚本就会自动安装编译Nginx、MySQL、PHP、phpMyAdmin、Zend Optimizer这几个软件。

安装时间可能会几十分钟到几个小时不等，主要是机器的配置网速等原因会造成影响。

**3、安装完成**

如果显示Nginx: OK，MySQL: OK，PHP: OK

![https://lnmp.org/images/1.3/lnmp-1.3-install-sucess.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-suces.png)

并且Nginx、MySQL、PHP都是running，80和3306端口都存在，并提示Install lnmp V1.3 completed! enjoy it.的话，说明已经安装成功。

访问方式：访问云主机公网IP

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-27.png)

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-28.png)

**4、安装失败**

![https://lnmp.org/images/1.3/lnmp-1.3-install-failed.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-lnmp-org-images-1-3-lnmp-1-3-install-faile.png)

如果出现类似上图的提示，则表明安装失败，说明没有安装成功！！需要用winscp或其他类似工具，将/root目录下面的lnmp-install.log下载下来，到京东云支持论坛发帖注明你的系统发行版名称及版本号、32位还是64位等信息，并将lnmp-install.log压缩以附件形式上传到论坛，我们会通过日志查找错误，并给予相应的解决方法。