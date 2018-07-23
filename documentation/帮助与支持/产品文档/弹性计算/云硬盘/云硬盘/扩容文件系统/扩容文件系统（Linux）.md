# **扩容文件系统（Linux）******

以 CentOS 操作系统为例，假设主机上已挂载一块 42.9GB 的硬盘，分区为 “/dev/vdb1” ，文件系统格式为 “ext4”，挂载位置是 “/home/test”，现在需要扩容到 53.7GB 。具体步骤如下 (需要 root 权限)：

**注意：扩容之前要备份好数据，避免因误操作等因素导致数据丢失。******

1、在控制台将硬盘从云主机上卸载，完成云硬盘扩容操作后重新挂载到云主机。

2、环境查看

1）使用fdisk -l 查看硬盘分区信息

![blob.png](https://img1.jcloudcs.com/cms/5dc55aa4-a878-483a-be81-0a73a9d06c8920170811185844.png)

2）可以看到/dev/vdb的磁盘容量为53.7GB，有一个分区/dev/vdb1，使用fdisk -l /dev/vdb1查看分区容量，可以看到/dev/vdb1的容量是42.9GB

![blob.png](https://img1.jcloudcs.com/cms/ca15412f-b6c7-42ba-a7d6-4b8576d058ca20170811185907.png)

3）使用df -h查看文件系统，可以看到挂载点为/home/test，且大小为40GB

### ![blob.png](https://img1.jcloudcs.com/cms/00931d79-3c69-4a16-9c83-fc65dd8af05e20170811185925.png)

3、下面开始对分区/dev/vdb1进行扩容

1）卸载文件系统
umount /home/test

2）扩大分区容量，此处以fdisk为例，也可使用parted来进行扩容，但两个命令不能混用，混用会导致起始扇区不一致。

fdisk /dev/vdb

依次键入p d n p 1 两次回车 wq

p: 打印分区信息

d: 删除分区

n: 新建分区

p: 新建分区的类型为主分区

1: 分区号为1

wq: 保存并退出

**注：保存之前请确定自己的操作无误，若发现有误操作，可键入q直接退出，此前操作都将无效。******

### ![blob.png](https://img1.jcloudcs.com/cms/a6fc27ef-0a49-46ff-9a7a-72416434a2c020170811190001.png)

3） 查看扩容后的分区容量
fdisk -l /dev/vdb1

![blob.png](https://img1.jcloudcs.com/cms/88f12aed-bdf3-4213-bc2e-da95bd4c6a0020170811190017.png)

分区容量已经扩大到53.7GB，但是此时文件系统还是原来的大小，下面两条命令是让文件系统扩展到与分区相匹配的大小。

4）检测文件系统正确性
e2fsck -f /dev/vdb1

![blob.png](https://img1.jcloudcs.com/cms/ff0f130b-f21e-44d8-84a9-bf31888413ee20170811190049.png)

5）重定义文件系统大小
resize2fs /dev/vdb1

![blob.png](https://img1.jcloudcs.com/cms/6631934d-a619-4938-81ea-c259f25f236f20170811190103.png)

6）mount /dev/vdb1 /home/test 将扩容好的文件系统挂载到挂载点/home/test

7）查看文件系统大小
df -h /dev/vdb1

![blob.png](https://img1.jcloudcs.com/cms/91e5d1c8-2c13-4ac5-8a8b-c6249897397b20170811190117.png)

可见文件系统已经扩展了。