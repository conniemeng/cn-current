**CentOS 5及CentOS 6系统**

三种办法可配置服务开机自启动：

ln -s 在/etc/rc.d/rc/*.d目录中建立/etc/init.d/服务的软连接(/*代表0～6七个运行级别之一）

chkonfig 命令行运行级别设置

ntsysv 伪图形运行级别设置

注意：

* 
上述三类方式主要用于CentOS 5及CentOS 6，其他版本未进行验证；
* 
若您不知道运行级别，请通过cat /etc/inittab操作查看/etc/inittab中的配置，如下图：

![](https://img1.jcloudcs.com/cms/cdfe1707-8b17-4b0f-979e-a009977ee63320170512154539.png)

如上图所示id:3:initdefault: 这里的3表示运行级别为3，完整的多用户模式。默认情况下都是在级别3下，如果安装了图形界面，那么运行级别为5。

![](https://img1.jcloudcs.com/cms/5102c7a2-1fd4-4a1b-8565-4f7ec91a31db20170512184901.png)

注：/etc/rc[0~6].d其实是/etc/rc.d/rc[0~6].d的软连接，是为了实现和Unix的兼容性

这7个目录中，每个目录分别存放着对应运行级别加载时需要关闭或启动的服务。由详细信息可知，每个脚本文件都对应着/etc/init.d/目录下具体的服务。

![](https://img1.jcloudcs.com/cms/ca1e0c43-ccb3-47e6-a8d1-7d4a962d7fa520170512184931.png)

K开头的脚本文件代表运行级别加载时需要关闭的，S开头的代表需要执行。因此，当我们需要开机启动自己的脚本时，只需要将可执行脚本放在/etc/init.d目录下，然后在/etc/rc.d/rc/*.d中建立软链接即可，操作示例如下：

[root@localhost ~]/# ln -s /etc/init.d/sshd /etc/rc.d/rc3.d/S100ssh

此处sshd是具体服务的脚本文件，S100ssh是其软链接，S开头代表加载时自启动。如果需要在多个运行级别下设置自启动，则需建立多个软链接。

这种方式比较繁琐，适用于自定义的服务脚本。如果系统中已经存在某些服务（比如安装apache时就会有httpd服务项），可以使用下面的两种方式

## **方法2：chkconfig 命令行**

![](https://img1.jcloudcs.com/cms/2c3c22c4-e1c8-402f-b775-6f724b2030f720170512185016.png)

如果需要自启动某些服务，只需使用chkconfig 服务名 on即可，若想关闭，将on改为off

在默认情况下，chkconfig会自启动2345这四个级别，如果想自定义可以加上--level选项

![](https://img1.jcloudcs.com/cms/cf1197fc-eeef-410b-8bd4-c13c613011eb20170512185038.png)

上图中先将sshd服务的所有启动级别关闭，然后使用--level选项启动自定义级别

**注****：********--list选项可查看指定服务的启动状态，chkconfig不带任何选项则查看所有服务状态**

## **方法3：ntsysv 伪图形**

ntsysv在chkconfig基础上加上了图形界面。启动ntsysv有两种方式，一是直接在命令行中输入ntsysv，二是使用setup命令，然后选择系统服务。

![](https://img1.jcloudcs.com/cms/95810a1c-3bc1-4b90-a706-5153b4a8831020170512185145.png)

默认情况下，在ntsysv中设置的启动服务的级别同当前运行级别。例如，当前的运行级别是3,那么在伪图形界面中选择启动服务后，它的运行级别也为3。若想自定义运行级别即可使用ntsysv --level方式

![](https://img1.jcloudcs.com/cms/1b4184cb-7470-4573-9bbf-08f947017f0b20170512185208.png)

以上三种操作需要保证服务脚本文件可执行，并且要有root权限。其中，第一种方式多用于自定义脚本，第二、三种多用于系统已存在的服务比如ftp、samba、ssh、httpd等等。并且，要做相关设置需要弄清楚运行级别的问题。此外若想手动启动某服务，传统的方式是 /etc/init.d 服务名 start，实际上还可以通过service 服务名 start实现，如下图所示：

![](https://img1.jcloudcs.com/cms/cbb89300-9bd4-403e-b14d-dfd8acc1380e20170512185322.png)