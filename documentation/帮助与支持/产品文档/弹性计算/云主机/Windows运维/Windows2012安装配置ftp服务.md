**Windows2012安装配置ftp服务**

注意：本文相关 Windows 配置及说明已在 Windows2012 64位操作系统中进行过测试。其它类型及版本操作系统配置可能有所差异，具体情况请参阅相应操作系统官方文档。

**安装**

1.选择左下角的服务器管理器。点击管理，添加角色和功能。

![1.png](https://img1.jcloudcs.com/cms/ccfec268-bf81-4cd6-9349-91f07c0c70a620170814111707.png)

![2.png](https://img1.jcloudcs.com/cms/d3f5f084-83b5-4c60-8c03-2c3ec57ecc7320170814111729.png)

2.默认下一步，在选择服务器角色中，勾选Web服务器（IIS），选择添加功能，下一步。

![6.png](https://img1.jcloudcs.com/cms/fec8db46-2548-434c-beb1-6a98629a2aa820170814112047.png)![7.png](https://img1.jcloudcs.com/cms/ffb0a650-ad00-41dc-8c9c-c11ed9ff04a120170814112052.png)

![8.png](https://img1.jcloudcs.com/cms/1be5683d-7c86-428f-8db6-553412c85ca520170814112338.png)

3.默认下一步，在选择角色服务中，勾选FTP服务器，FTP服务，选择下一步进行安装。

![11.png](https://img1.jcloudcs.com/cms/29c58234-68f0-4772-a4dd-1345d789d25a20170814112849.png)

![12.png](https://img1.jcloudcs.com/cms/7c2899ea-b8ab-4275-8f55-0f476192d87720170814112939.png)

![13.png](https://img1.jcloudcs.com/cms/776b6fe6-7a74-4961-9144-0cdb4f8ad7da20170814113011.png)

**配置**

1.服务器管理器，选择工具，Internet Information Services（IIS）管理器。

![14.png](https://img1.jcloudcs.com/cms/198143b2-8b4c-41f0-b8ba-5c6aeac0d3d820170814113708.png)

2.左侧栏右键网站，选择添加FTP站点。

![15.png](https://img1.jcloudcs.com/cms/a574eba6-3cb9-4d3c-b425-613457e8f02d20170814114137.png)

3.设置ftp站点名称和ftp内容目录物理路径。

![16.png](https://img1.jcloudcs.com/cms/dcd2d34c-5fdd-49fe-991c-532136bfb92420170814114405.png)

4.设置ftp默认端口为21，选择无SSL。

![17.png](https://img1.jcloudcs.com/cms/9b32abb8-d434-40e9-bfca-5fc4d38db38920170814114615.png)

5.身份验证选择基本，允许访问设置为指定用户，填写ftp用户名，添加读取和写入权限。

![18.png](https://img1.jcloudcs.com/cms/80a1dbc0-1a06-45d0-86a9-6e2e23586af520170814114757.png)

6.服务器管理器，选择工具，计算机管理。

![19.png](https://img1.jcloudcs.com/cms/8d83b557-71de-4da3-9edf-d0fe571fec5b20170814144034.png)

7.本地用户和组，右键用户，选择新用户。创建ftp用户，设置密码。

![1.png](https://img1.jcloudcs.com/cms/1ba3add7-ef53-4e0c-bac1-7e71cff3871120171025151013.png)

![21.png](https://img1.jcloudcs.com/cms/dce4d6ab-046a-4c82-be30-535501d01f8320170814144408.png)

8.右键ftp内容目录，选择属性。

![22.png](https://img1.jcloudcs.com/cms/61e3839e-01a3-4e55-99f3-2c0a04d62ecd20170814144619.png)

9.选择安全，编辑，添加。

![23.png](https://img1.jcloudcs.com/cms/08b463b8-71f1-4a82-b507-2f8af139428220170814144722.png)

![24.png](https://img1.jcloudcs.com/cms/afbfd5c8-3b03-4c83-915b-7d6ab77f543220170814144739.png)

10.选择高级，立即查找，选择ftp用户。

![25.png](https://img1.jcloudcs.com/cms/034809fb-4677-4775-9cef-3d10c8b916fc20170814144946.png)

![26.png](https://img1.jcloudcs.com/cms/003f9c02-66c6-4fe8-bcb8-4eee273dcb4e20170814145014.png)

![27.png](https://img1.jcloudcs.com/cms/e06a34f3-1a92-4dcd-9141-8c0cfe82e45920170814145027.png)

11.给ftp用户添加读取和写入权限。

![28.png](https://img1.jcloudcs.com/cms/e519883c-fcdf-4a6b-bf59-0302ee1c8fa420170814145111.png)

**防火墙配置**

1.左下角开始，打开控制面板。

![29.png](https://img1.jcloudcs.com/cms/eb1d3a38-0eeb-477d-a8e1-2f204990610520170814151953.png)

2.选择windows防火墙，高级设置。

![30.png](https://img1.jcloudcs.com/cms/5935edf1-81cc-4299-8bc3-eef0dac21a5920170814152109.png)

![31.png](https://img1.jcloudcs.com/cms/fe1dda6d-47b5-4eb1-a57a-74e83cc5749720170814152135.png)

3.左侧选择入站规则，右侧选择新建规则。

![32.png](https://img1.jcloudcs.com/cms/aa50ca32-405c-4d9e-9507-4ab22b21250620170814152257.png)

4.选择端口，输入ftp服务的默认端口21，选择允许连接，输入规则名称，完成。

![33.png](https://img1.jcloudcs.com/cms/45d4a1ee-9f50-45eb-8f11-0b688abc838620170814152702.png)

![34.png](https://img1.jcloudcs.com/cms/b1757933-8ed0-43db-ab99-d5f824c5e34220170814152722.png)![35.png](https://img1.jcloudcs.com/cms/0b2b0110-1c4b-4441-9558-60c0f8cd56df20170814152742.png)

![36.png](https://img1.jcloudcs.com/cms/994f9bbf-3b96-41d4-8840-aa77022e578420170814152756.png)

5.控制面板，windows防火墙，允许应用或者功能通过Windows防火墙。

![37.png](https://img1.jcloudcs.com/cms/914bb5ea-a13f-4fe8-8955-7be56071c11420170814153743.png)

6.选择允许其他应用，浏览。

![38.png](https://img1.jcloudcs.com/cms/02c23404-e09f-4dfd-bd41-b97e06f0595120170814153835.png)

![39.png](https://img1.jcloudcs.com/cms/cd75ced0-9986-4eca-a83e-55fc69d480d420170814153904.png)

7.找到"C:\Windows\System32\svchost.exe"，双击选择添加。

![40.png](https://img1.jcloudcs.com/cms/b108dc38-ba50-4d8e-b2d5-730b2cd8cbb320170814154105.png)

![41.png](https://img1.jcloudcs.com/cms/cf09fd01-5fcf-4ea5-89df-6b9407047f9e20170814154138.png)

至此ftp服务和防火墙配置完成。

如无法解决您的问题，请向我们提工单。