# **snapshot create**

Usage: jcloud snapshot create [OPTIONS] -v volume
Create a snapshot from a volume
-f, --force Force to create snapshot, needed if volume is in use
--help=false Print usage
--name= Specify snapshot name
-v, --volume Specify volume to create snapshot

基于硬盘创建一个新的快照。如果没有指定快照名称，则京东云容器服务会生成一个随机id：

$ jcloud snapshot create --name db-snapshot db-vol
db-snapshot

快照仅能保留执行快照命令时已写入云硬盘的数据。不会保存任何被容器缓存的数据。您可以对正在使用的硬盘制作快照。但是，为了确保快照的一致性和完整性，最好先停止容器，快照制作完成后再启动容器。

快照名称必须是唯一的。也就是说，不能有两个不同的快照使用相同的快照名称。如果快照名称重复，jcloud 会返回错误：
A snapshot named "db-snapshot" already exists. Choose a different snapshotname.