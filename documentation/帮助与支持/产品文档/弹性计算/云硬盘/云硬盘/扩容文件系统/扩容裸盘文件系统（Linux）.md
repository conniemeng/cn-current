# **扩容裸盘文件系统（Linux）**

如果之前并未对硬盘执行过分区操作，可以参考如下方法，直接对硬盘文件系统进行扩容：

1.在控制台完成云硬盘[升级容量](http://www.jcloud.com/help/detail/508/isCateLog/1)操作；

2.执行[挂载云硬盘](http://www.jcloud.com/help/detail/505/isCateLog/1)，确保云硬盘处于“已挂载”状态；

3.使用fdisk -l 查看硬盘分区信息；

![fdisk -l.jpg](https://img1.jcloudcs.com/cms/33b92221-a7a2-46d2-ab38-175e4f23f74920170920095517.jpg)

4.使用df -h查看挂载信息；

![df -h.jpg](https://img1.jcloudcs.com/cms/48fb54e8-b66b-4943-bb64-34e04ab6281120170920095531.jpg)

5. 执行umount操作取消挂载；

![umount.jpg](https://img1.jcloudcs.com/cms/c6614340-b071-4586-94c8-8142744e21df20170920095543.jpg)

6.执行e2fsck -f /dev/vdb检测文件系统正确性；

![e2fsck.jpg](https://img1.jcloudcs.com/cms/cca5d0be-ef6a-46dc-a316-8f7d4519436a20170920095706.jpg)

7.执行resize2fs /dev/vdb重新定义文件系统大小；

![resize2fs.jpg](https://img1.jcloudcs.com/cms/b9808e04-7bd5-4cd7-a414-02dee28c0c2b20170920095601.jpg)

8. 执行mount /dev/vdb /mnt重新挂载磁盘，可以看到磁盘已经扩容成功。

![mount.jpg](https://img1.jcloudcs.com/cms/328cb44f-1dcb-41aa-9b89-568c6e44db5720170920095613.jpg)