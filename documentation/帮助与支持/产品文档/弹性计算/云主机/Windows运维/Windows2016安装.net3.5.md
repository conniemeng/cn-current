**Windows2016安装.net3.5报错**

**问题现象：**

默认下安装.net3.5会安装失败，提示找不到源文件。如图：

![1.png](https://img1.jcloudcs.com/cms/457b6200-f67c-4603-8338-bc589b7f159620180709162720.png)

**问题原因：**

Windows update服务没有运行导致。

**解决方法：**

开始菜单运行执行services.msc回车，找到windows update服务。默认是禁用，改成手动并启动。然后在线安装.net3.5组件，安装完毕后可以视需求，停止及禁用windows update服务。

![2.png](https://img1.jcloudcs.com/cms/4cef3049-327b-4579-9174-0555ea672b2120180709162949.png)

如无法解决您的问题，请向我们提工单。