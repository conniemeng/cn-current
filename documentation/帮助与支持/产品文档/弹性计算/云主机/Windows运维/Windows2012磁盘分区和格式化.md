**Windows2012磁盘分区和格式化**

注意：磁盘分区和格式化是高风险行为，请慎重操作。如下操作是针对新购买的数据盘，如果涉及到原有数据盘的处理，请务必对云主机的数据盘创建快照以避免可能的数据丢失。

**购买数据盘后，默认是没有分区、格式化的，您可以参考以下方法来进行初始配置：**

1.右键左下角开始，选择磁盘管理。选择MBR（主启动记录），确认。

![1.png](https://img1.jcloudcs.com/cms/2461e38b-3d31-402c-9171-0b1e820609a420170904161305.png)

![2.png](https://img1.jcloudcs.com/cms/e491a2a1-c06a-442e-ab50-6d7faca09c6020170904161526.png)

2.在空白分区上，右键选择【新建简单卷】。

![3.png](https://img1.jcloudcs.com/cms/a2c33dee-bbb4-4727-a19e-13685dce271520170904161841.png)

3.默认下一步。

![4.png](https://img1.jcloudcs.com/cms/e2f00cc8-295b-48f3-9b18-5ad13741500320170904161905.png)

![5.png](https://img1.jcloudcs.com/cms/1a93be93-3bdc-48a7-a066-7a7af7cbb4de20170904161914.png)

4.选择数据盘挂载的盘符，下一步。

![6.png](https://img1.jcloudcs.com/cms/048b8ded-3963-47dc-a710-bc6348e77e7420170904162012.png)

5.选择文件系统为NTFS，勾选执行快速格式化。

![7.png](https://img1.jcloudcs.com/cms/7f71ad52-f995-46ae-86f2-23136211d62f20170904162109.png)

6.点击【完成】，系统会自动设置好新的分区。数据盘挂载盘符格式化完毕。

![8.png](https://img1.jcloudcs.com/cms/52da8519-4109-457d-9b1e-5b1c799b946f20170904162229.png)

如无法解决您的问题，请向我们提工单。