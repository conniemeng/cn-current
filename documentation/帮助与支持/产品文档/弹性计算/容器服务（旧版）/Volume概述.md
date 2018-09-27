# **Volume概述**

在京东云, volume即云硬盘，为容器服务提供了高可用，高性能的持久化存储服务。云硬盘实现了多副本，从而保证服务的可靠性。

Volume 使用EXT4 文件系统。京东云为每个容器创建容量为10GB的系统盘。

京东云提供的云硬盘独立于容器的生命周期。
$ jcloud volume create --size=10 --name=dbdata
dbdata

**基于快照创建新硬盘**

新硬盘保留原始快照的全部数据，硬盘大小与快照大小相同:
$ jcloud volume create --snapshot=mysnapshot --name=dbdata
dbdata

**使用

jcloud run
为容器挂载volumes**

$ jcloud run -v dbdata:/opt/data/ --name mycontainer ubuntu
mycontainer

**在一个容器的不同挂载点上挂载相同的volume。**

$ jcloud run -v vol1:/opt/data -v vol1:/opt/log --name=mycontainer ubuntu
mycontainer

**使用jcloud run创建硬盘**

/# 创建空volume (10GB)并挂载到 /container/path
$ jcloud run -v /container/path --name mycontainer ubuntu
mycontainer
/# 创建容量为10GB的volume并上传/local/path中的数据
$ jcloud run -v /local/path/:/container/path --name mycontainer ubuntu
mycontainer
/# 创建容量为10GB的volume并上传git://url[:branch]中的数据
$ jcloud run -v git://url[:branch]:/container/path --name mycontainer ubuntu
mycontainer
/# 创建容量为10GB的volume并上传 http://url.git[:branch]中的数据
$ jcloud run -v http://url.git[:branch]:/container/path --name mycontainer ubuntu
mycontainer
/# 创建容量为10GB的volume并上传 http://url中的数据
$ jcloud run -v http://url:/container/path --name mycontainer ubuntu
mycontainer

**Volume 大小**

volume容量范围为10到500 GB.

**Volume 生命周期**

将volume挂载到容器之后，volume的生命周期与容器的生命周期相关联。重启或启动容器时，不需要重复对volume进行挂载操作。一块volume仅能挂载到一台容器。

当执行jcloud

rm删除容器时
，挂载到容器的volume会被自动卸载。创建容器时被自动分配的系统盘会同时被删除：
$ jcloud rm -v db_container
db_container

Volume 切换

切换volume之前，需要执行jcloud rm或jcloud stop命令，停止或删除volume挂载的容器之后，再将volume挂载到新的容器上。
$ jcloud rm db_contaienr
db_container
$ jcloud run -v dbdata:/opt/data --name new_db ubuntu
new_db

Volume只能挂载到当前地域下的容器上。

**Volume的重用**

注意：请注意volume的访问限制。

例如，如果volume 被挂载到名称为foo的容器上之后，被名称为bar的容器重用。volume的文件或路径限制与在容器foo中的设置保持一致。因此，改变容器用户(uid/gid pair)可能会影响volume的访问权限。

**镜像存储盘创建**

如果 容器镜像中包含volume说明。启动容器时会自动创建一个新的volume。
$ jcloud run --name mycontainer jcloudhq/noauto_volume_test
mycontainer
$ jcloud volume ls
DRIVER VOLUME NAME SIZE CONTAINER
jcloud d358e606246ce22c9d528913f6990c45cd8ddbb7df7d8e1110d3c66b0cbf734 10 GB 1b617eb3ab0f
jcloud 805ef123f4e60b048448784a4aa56d13469fb4aa42ae0e1fcd006c2b7b1e807 10 GB 1b617eb3ab0f

你可以通过增加

--noauto-volume
参数取消自动创建volume。

$ jcloud run --name mycontainer --noauto-volume
jcloudhq/noauto_volume_test

**文件Volume的初始化**

volume可以基于一个指定的文件源（local或http）被初始化，相应的volume端也必须指定一个文件，如果目标文件不存在，在执行初始化操作时将会被自动创建。

注意：如果volume的目标文件包含镜像本身的文件路径，容器将会启动失败。例如：执行如下命令将会导致容器启动失败，因为/etc/hosts是一个文件源，/mnt路径包含在容器镜像ubuntu:14.04中。以上规则同样适用于基于http/https的远程volume源。
$ jcloud run -d -v /etc/hosts:/mnt ubuntu:14.04

指定一个non-directory路径挂载源文件可以避免容器启动失败，参考示例：

$ jcloud run -d -v /etc/hosts:/mnt/hosts ubuntu:14.04