**Windows2012设置远程桌面不断开**

左下角选择开始

![1.png](https://img1.jcloudcs.com/cms/197ccb63-5741-4d33-b558-e47bf1d09d7720180208162539.png)

选择运行

![2.png](https://img1.jcloudcs.com/cms/284ef119-03eb-4a61-909d-314637b6b2c520180208162555.png)

输入gpedit.msc

![3.png](https://img1.jcloudcs.com/cms/82a18b8d-285b-4fd2-9147-9644495f57c920180208162628.png)

依次选择计算机配置--管理模板--windows组件--远程桌面服务--远程桌面会话主机--会话时间限制。

![4.png](https://img1.jcloudcs.com/cms/33c5e0b3-9700-40e3-aa0b-b062cdadf92920180208162752.png)![5.png](https://img1.jcloudcs.com/cms/c412eae2-05e9-4089-a2f8-baf60b5f41e520180208162801.png)

右侧5个选项都选择已禁用，应用。

![6.png](https://img1.jcloudcs.com/cms/546d197f-46f4-477b-8455-2bda7b24d46620180208162954.png)