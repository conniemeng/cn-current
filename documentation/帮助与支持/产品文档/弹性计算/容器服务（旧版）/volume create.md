# **volume create**

Usage: jcloud volume create [OPTIONS]
Create a volume
--help=false Print usage
--name= Specify volume name
--size= Specify volume size (a multiple of 10 GB, up to 1TB)
--snapshot= Specify snapshot id or name to restore

创建新硬盘以供容器使用和存储数据。如果没有指定volume名称，则京东云容器服务会生成一个随机id。你可以创建一个新硬盘，然后将硬盘挂载到容器，例如：

$ jcloud volume create --name hello
hello

也可以基于快照创建一块硬盘：

$ jcloud volume create --name new-vol --snapshot=db-snapshot
new-vol

新硬盘的大小与快照大小相同。

硬盘的名称必须是唯一的。也就是说，两个不同的硬盘不能使用相同的名称。如果硬盘名称重复，

jcloud
命令会返回错误：
A volume named "hello" already exists. Choose a different volumename.