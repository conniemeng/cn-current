**云服务器Linux SWAP配置概要说明**

Linux 中的 SWAP（交换分区），类似于 Windows 的虚拟内存。系统会把一部分硬盘空间虚拟成内存使用，将系统内非活动内存换页到 SWAP，以提高系统可用内存。

注： 使用须知，云服务器 如果您使用普通云盘，不建议使用swap分区。如果是高效云盘或SSD云盘，可以根据实际情况使用swap分区。

创建swap分区是为了弥补物理内存的不足，也就是虚拟内存的概念，把硬盘的一部分划分作为虚拟内存，但这个空间不是越大越好，硬盘的速度远低于内存，设置不当反而拖慢系统的速度。

# ![]()**SWAP 配置介绍及 FAQ**

·开启SWAP

·关闭SWAP

·CentOS使用mkswap格式化文件时报错的处理方法

京东云的主机默认没有swap分区，可以使用free命令查看：

![](https://img1.jcloudcs.com/cms/440273a8-a50c-4b86-b12b-37367f2bb38d20170602105925.png)

## ![]()**开启 SWAP**

1、创建用于交换分区的文件：

ddif=/dev/zero of=/mnt/swap bs=block_size count=number_of_block

**注**：block_size、number_of_block大小可以自定义，比如 bs=1M count=1024代表设置 1G大小 SWAP分区。

![](https://img1.jcloudcs.com/cms/849face6-1796-4f18-a381-528336c013fa20170602110011.png)

2、设置交换分区文件：

mkswap/mnt/swap

![](https://img1.jcloudcs.com/cms/26fd388c-05e4-4f83-b8f6-563f016685cf20170602110137.png)

3、立即启用交换分区文件

swapon/mnt/swap

![](https://img1.jcloudcs.com/cms/0788f0a5-9e7e-42df-beba-47d6feb7409d20170602110859.png)

**注**：如果在/etc/rc.local中有*swapoff -a*需要修改为*swapon–a*

**[root@softwaretest ~]/# vi /etc/rc.loca

![](https://img1.jcloudcs.com/cms/39db1725-4510-4d6e-8e6b-73a27301201220170602111037.png)

4、设置开机时自启用 SWAP 分区：

需要修改文件/etc/fstab中的SWAP行，添加

[root@softwaretest~]/# vi /etc/fstab

/mnt/swap swapswap defaults00

![](https://img1.jcloudcs.com/cms/3500dfe8-dceb-4b46-95b5-22c707fc7e8b20170602111103.png)

**注**：/mnt/swap 路径可以修改，可以根据创建的 SWAP 文件具体路径来配置。

5、修改swpapiness参数

在Linux系统中，可以通过查看/proc/sys/vm/swappiness内容的值来确定系统对SWAP分区的使用原则。当swappiness内容的值为0时，表示最大限度地使用物理内存，物理内存使用完毕后，才会使用SWAP分区。当swappiness内容的值为100时，表示积极地使用SWAP分区，并且把内存中的数据及时地置换到SWAP分区。

查看修改前为 0，需要在物理内存使用完毕后才会使用 SWAP 分区：

![](https://img1.jcloudcs.com/cms/c4f6e246-d6e1-4feb-a80b-879ba49b45ca20170602111352.png)

可以使用下述方法临时修改此参数，假设我们配置为空闲内存少于 10% 时才使用 SWAP 分区：

echo10>/proc/sys/vm/swappiness

![](https://img1.jcloudcs.com/cms/ae14de27-d08d-4dfb-b155-026936ab012c20170602111533.png)

若需要永久修改此配置，在系统重启之后也生效的话，可以修改 /etc/sysctl.conf 文件，并增加以下内容：
/# vim /etc/sysctl.conf
vm.swappiness=10

/# sysctl -p
## ![]()**关闭 SWAP**

当系统出现内存不足时，开启 SWAP 可能会因频繁换页操作，导致 IO 性能下降。如果要关闭 SWAP，可以采用如下方法。

1、*free**-m*查询SWAP分区设置
![](https://img1.jcloudcs.com/cms/46f1fc55-20aa-40bd-97f8-37cd6c49969220170602111703.png)

2、使用命令swapoff关闭SWAP，比如：

swapoff/mnt/swap

![](https://img1.jcloudcs.com/cms/d7c59ba8-c132-45b0-9c6e-307c78e30f8a20170602111737.png)

3、修改/etc/fstab文件，删除或注释相关配置，取消SWAP的自动挂载：

![](https://img1.jcloudcs.com/cms/e5e4a635-b98c-461c-bcef-06495bb418b520170602111819.png)

4、 通过free -m **确认 SWAP 已经关闭。

![](https://img1.jcloudcs.com/cms/8369ca18-ec3f-459b-9e58-11cc4c052f4620170602111854.png)

5、swappiness参数调整：

可以使用下述方法临时修改此参数，这里配置为 0%：
1. echo 0 >/proc/sys/vm/swappiness

若需要永久修改此配置，在系统重启之后也生效的话，可以修改 /etc/sysctl.conf 文件，并增加以下内容：

1. /# vim /etc/sysctl.conf2. vm.swappiness=03. /# sysctl -p
## ![]()**CCentos 使用 mkswap 格式化文件时报错的处理方法**

### **问题现象**使用mkswap创建SWAP时出现类似如下报错信息：

1. mkswap: error: swap area needs to be at least 40 KiB

### **问题原因**

指定的SWAP文件太小，SWAP文件至少应该大于40KB。

### **解决方法**

重新生成更大的文件格式化为SWAP即可。

如果问题还未能解决，您可以到京东云社区进行免费咨询，或联系售后技术支持。