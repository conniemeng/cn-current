**Windows2008安装配置ftp服务**

注意：本文相关 Windows 配置及说明已在 Windows2008 64位操作系统中进行过测试。其它类型及版本操作系统配置可能有所差异，具体情况请参阅相应操作系统官方文档。

**安装**

1.选择左下角的服务器管理器。点击角色，添加角色。

![1.png](https://img1.jcloudcs.com/cms/1c39e8f7-ed8d-43bd-ba1e-aebf6c1cfccc20170818133453.png)

![2.png](https://img1.jcloudcs.com/cms/0f1479eb-9256-4e08-ab7a-7d7f5b3099d520170818133527.png)

2.默认下一步，在选择服务器角色中，勾选Web服务器（IIS）。

![3.png](https://img1.jcloudcs.com/cms/1675242c-b890-49c6-9f61-7e905442180c20170818133752.png)

3.默认下一步，在选择角色服务中，勾选FTP服务器。

![4.png](https://img1.jcloudcs.com/cms/97d2a2ff-8d16-481e-94e0-a7d2f4118af020170818134035.png)

4.默认下一步，点击安装，直到完成。

![5.png](https://img1.jcloudcs.com/cms/6f08a6a8-3ef0-466c-bdde-9ee6a9be6b3f20170818134154.png)

**配置**

1.服务器管理器，点击左侧栏的角色，Web服务器（IIS），Internet信息服务（IIS）管理器。右键中间栏的主机名选项，选择添加FTP站点。

![6.png](https://img1.jcloudcs.com/cms/83f2280d-ac15-4b24-bf8d-1124662a7a3820170818134630.png)

2.设置FTP站点名称，和FTP内容目录物理路径。

![7.png](https://img1.jcloudcs.com/cms/1e58cead-1277-4e3f-9d16-84b4702e10e520170818134916.png)

3.设置FTP服务端口为默认的21端口，ssl勾选无。

![8.png](https://img1.jcloudcs.com/cms/1a711111-6c58-4366-a5df-6e61eb27f1ea20170818135115.png)

4.身份验证选择基本，指定用户，填写ftp账户名称，赋予读取和写入权限。

![9.png](https://img1.jcloudcs.com/cms/20147355-3e37-4f30-a2e6-bbe4eecf26f020170818135327.png)

5.服务器管理器，配置，本地用户和组，右键用户，选择新用户。

![10.png](https://img1.jcloudcs.com/cms/f5bcf196-3af4-4843-9034-5bc1fcaca2b720170818142222.png)

6.设置ftp用户名和密码。

![11.png](https://img1.jcloudcs.com/cms/561fb8ca-617c-4776-ae2d-489864d4c36220170818142537.png)

7.右键ftp内容目录，选择属性。

![12.png](https://img1.jcloudcs.com/cms/64439df9-4f53-4846-8867-9518d6cad33320170818142708.png)

8.选择安全，编辑。

![13.png](https://img1.jcloudcs.com/cms/762b235e-ba0c-4e60-aa7a-d7dff019dee320170818143401.png)

9.选择添加。

![14.png](https://img1.jcloudcs.com/cms/904778d9-0f62-4d80-b24e-1a1ebd646f5320170818143540.png)

10.选择高级，立即查找，找到ftp账户，选择确定。

![15.png](https://img1.jcloudcs.com/cms/874236c6-9ddd-43a8-9ee7-b5192264c0a220170818143728.png)

![16.png](https://img1.jcloudcs.com/cms/3b062cff-2e50-4ab2-997b-c4c5db1d7dbb20170818143750.png)

![17.png](https://img1.jcloudcs.com/cms/2a891af0-f867-4044-bc05-7348a40dbd6b20170818144602.png)

11.赋予ftp账户读取和写入权限。

![18.png](https://img1.jcloudcs.com/cms/aed4aa39-b73b-4906-b7e1-a6b843f6b29720170818144853.png)

**防火墙配置**

1.左下角开始，控制面板。

![19.png](https://img1.jcloudcs.com/cms/83922fca-b0b4-4d89-8283-72184f0b041e20170818145511.png)

2.双击windows防火墙，选择高级设置。

![20.png](https://img1.jcloudcs.com/cms/84651ffd-fd51-4f24-adb1-9d09edb9fddb20170818145637.png)

![21.png](https://img1.jcloudcs.com/cms/05fb1221-533e-4c7a-b6a8-9cc60cbe913e20170818145650.png)

3.左侧栏选择入站规则，右侧栏选择新建规则。

![22.png](https://img1.jcloudcs.com/cms/b31384ec-d48f-4e5d-8f57-d2ae61d0c80a20170818145825.png)

4.选择端口，本地特定端口，填写21。

![23.png](https://img1.jcloudcs.com/cms/194bc387-cc98-4bf1-8cbb-833e4d59d2eb20170818150007.png)

![24.png](https://img1.jcloudcs.com/cms/13ba5f1e-ed7c-4414-ad78-d0e729894d3e20170818150029.png)

5.选择允许连接，填写名称，完成。

![25.png](https://img1.jcloudcs.com/cms/ac4c3745-705a-43f5-b3e0-01fd0fbcaef620170818150122.png)

![26.png](https://img1.jcloudcs.com/cms/42fa61e5-88cf-4e27-9885-aa48b641a30820170818150132.png)

至此ftp服务和防火墙配置完成。

如无法解决您的问题，请向我们提工单。