**Windows2008磁盘分区和格式化**

注意：磁盘分区和格式化是高风险行为，请慎重操作。如下操作是针对新购买的数据盘，如果涉及到原有数据盘的处理，请务必对云主机的数据盘创建快照以避免可能的数据丢失。

**购买数据盘后，默认是没有分区、格式化的，您可以参考以下方法来进行初始配置：**

1.点击左下角的服务器管理器。

![1.png](https://img1.jcloudcs.com/cms/65bab767-bf18-4ea0-aa5a-3ba638ead44020170904111603.png)

2.选择【存储】--【磁盘管理】。

![2.png](https://img1.jcloudcs.com/cms/3f0687aa-9db6-4a00-b123-5621e98127d420170904111644.png)

3.右键点击数据盘（磁盘1），选择初始化磁盘。选择MBR（主启动记录），确定。

注：此时如果数据盘显示“脱机”，需先在磁盘1处右键点击“联机”再进行后续操作。

![3.png](https://img1.jcloudcs.com/cms/966ae670-4102-4b7f-b1a3-9da396f0393220170904111925.png)

![4.png](https://img1.jcloudcs.com/cms/588554ce-44c9-43a6-ae96-15e0734f2ffd20170904112704.png)

4.在空白分区上，右键选择【新建简单卷】。

![5.png](https://img1.jcloudcs.com/cms/12be6e81-f29b-4535-8f28-6a27ab35936220170904112808.png)

5.默认下一步。

![6.png](https://img1.jcloudcs.com/cms/4f9c47ef-791f-48bd-a8da-9fbe78f3585620170904112835.png)

![7.png](https://img1.jcloudcs.com/cms/c63a9fbd-1ce3-4815-97f1-033c366e084020170904112842.png)

6.选择数据盘挂载的盘符，下一步。

![8.png](https://img1.jcloudcs.com/cms/09aeccd3-d178-4742-8d2a-178ef10abbd520170904112922.png)

7.选择文件系统为NTFS，勾选执行快速格式化。

![9.png](https://img1.jcloudcs.com/cms/54dd882f-fc5d-4eeb-95ec-d1258f27f7a220170904113057.png)

8.点击【完成】，系统会自动设置好新的分区。数据盘挂载盘符格式化完毕。

![10.png](https://img1.jcloudcs.com/cms/d0f48b73-b603-4df5-85a4-a43605fe4dd720170904113156.png)

如无法解决您的问题，请向我们提工单。