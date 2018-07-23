1.通过云主机页面上的VNC登录Windows Server系统远程桌面；

![](https://img1.jcloudcs.com/cms/bc82fca7-ab97-451f-855a-97c4a5ad83d420170313113129.png)

2.登录系统桌面后，右键点击“计算机”，在弹出菜单中选择“管理”，在“服务器管理器”左侧界面点击“角色”，点击左侧“添加角色”；

![](https://img1.jcloudcs.com/cms/d4a0b1d7-b013-4c42-8da8-fcee8360a89820170313113136.png)

3.点击“下一步”；

![](https://img1.jcloudcs.com/cms/92b6726e-7126-45db-99fc-3c1fb703ceff20170313113143.png)

4.选择角色列表中的“Web服务器（IIS）”和“应用程序服务器”；

![](https://img1.jcloudcs.com/cms/441b85ea-35d9-4162-8502-73f646059fd220170313113150.png)

5.点击“添加必须的功能”按钮后，点击“下一步”；

![](https://img1.jcloudcs.com/cms/4b7fda2e-63be-4058-9d6e-3d5cc033d3a220170313113203.png)

6.点击“下一步”；

![](https://img1.jcloudcs.com/cms/0165dc7c-92af-4de5-ae05-d249cea9628a20170313113304.png)

7. 点击“下一步”；

![](https://img1.jcloudcs.com/cms/7351df10-84e9-45ee-9b19-5bd74a7deeb520170313113314.png)

8.点击“下一步”；

![](https://img1.jcloudcs.com/cms/5a8f39bb-59b7-4e69-999c-7ed8fda2efe420170313113321.png)

9.点击“安装”；

![](https://img1.jcloudcs.com/cms/23b25356-a02f-4873-aa7b-06826769925e20170313113328.png)

10.安装完成，点击“关闭”按钮；

![](https://img1.jcloudcs.com/cms/9ec113ce-e454-42fc-8efb-36a54b8df6ea20170313113334.png)

11.新创建一个文件夹，并使用记事本在该文件夹中创建一个名为index.html的文件；

![](https://img1.jcloudcs.com/cms/318e8c0c-7b82-461e-b308-e139c09eef1620170313113340.png)

12.打开“开始”-“管理工具”-“Internet信息服务（IIS）管理器”；

![](https://img1.jcloudcs.com/cms/518909a1-8124-48fc-a67e-9e92aed66f0c20170313113346.png)

13.右键点击“网站”，选择“添加网站”；

![](https://img1.jcloudcs.com/cms/8467786b-5d3e-4cde-b13a-56e7a23f261520170313113352.png)

14.在添加网站页面填写网站名称、物理路径、IP地址、端口号以及主机名；

![](https://img1.jcloudcs.com/cms/d39afb98-5815-4d0a-8751-57bcbdc378cf20170313113358.png)

15.从客户端浏览器访问该网站IP地址或域名，可以看到IIS服务器配置成功。

![](https://img1.jcloudcs.com/cms/fd4d23ed-8f86-442f-a75d-f778661c508e20170313113406.png)

至此，您已经在京东云上成功部署了Web环境，可以制作和发布站点了。