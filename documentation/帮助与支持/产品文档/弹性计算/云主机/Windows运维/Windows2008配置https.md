**Windows2008 iis服务配置https**

创建证书：

1、使用Windows Server 2008 R2的CA服务来创建证书，通过“服务器管理器”中的“添加角色”。

![1.png](https://img1.jcloudcs.com/cms/82aa4b71-c14e-445d-9e27-c7ed28b7524520180408132748.png)

![2.png](https://img1.jcloudcs.com/cms/f50665d5-7dee-4f2e-b2c5-26929af4936f20180408132754.png)

2、选择“Active Directory 证书服务”。

![3.png](https://img1.jcloudcs.com/cms/9d33b10d-d430-4b15-84d4-b23dd3c73aa820180408132834.png)

3、添加服务的时候需要选择：“证书颁发机构”“证书颁发机构Web注册”“联机响应程序”三个服务。

![4.png](https://img1.jcloudcs.com/cms/0322f87e-b91e-433a-8d29-3078e0d4617220180408132925.png)

4、因为不是域控环境，所以选择“独立（A）”即可。

![5.png](https://img1.jcloudcs.com/cms/5386e8c8-b010-41e4-9e53-4b317ab96f5520180408133034.png)

5、安装的第一个CA，选择“根CA（R)”即可。

![6.png](https://img1.jcloudcs.com/cms/ae0bd677-1086-4bc7-b123-fbb81532b3b920180408133139.png)

6、选择“新建私钥（R）”即可。

![7.png](https://img1.jcloudcs.com/cms/c96db925-1d29-47c0-9ecb-879ab4b87c8920180408133234.png)

7、这里保持默认即可，当然如果需要自定义的设置，也可以自行选择。

![8.png](https://img1.jcloudcs.com/cms/9033e164-20b1-4bb4-a214-6169bd0e45d120180408133357.png)

8、此处的CA名称，建议保持默认即可。

![9.png](https://img1.jcloudcs.com/cms/f3d3096a-53a7-4e86-a1b4-2c3dda6335a720180408133447.png)

9、设置证书的时间，默认是5年，这个可以根据Web的情况，自行设置。

![10.png](https://img1.jcloudcs.com/cms/66cb8855-78d2-403c-bc97-c6ba97870aed20180408133522.png)

10、设置证书数据库位置和日志位置，自行选择即可。

![11.png](https://img1.jcloudcs.com/cms/1026a3d2-8145-47ea-81bc-12133721481620180408133617.png)

**创建IIS服务：**

1、安装好CA证书后，安装程序会自动引导开始IIS的安装。

![12.png](https://img1.jcloudcs.com/cms/115a9a22-ebb1-4404-9c70-24e6dcba188820180408133824.png)

2、这个里需要勾选“ASPNETt”和“.NET 扩展性”。

![13.png](https://img1.jcloudcs.com/cms/fe4d46d1-b41b-4cd9-a9b6-f20c13549f7620180408134013.png)

3、需要说明的是，安装了证书后，不能更改计算机名或域名。

![14.png](https://img1.jcloudcs.com/cms/737675d8-c957-4dc3-a03a-d141473ae22c20180408134139.png)

4、最后，确保证书服务和Web服务器IIS是安装成功的。

![15.png](https://img1.jcloudcs.com/cms/97c8cacb-d0bc-4a17-9a41-578ceccbe5cc20180408134212.png)

**创建自签名证书：**

1、在IIS管理器中选择“服务器证书”。

![16.png](https://img1.jcloudcs.com/cms/0095b84d-ba4c-438f-b366-0387080a1fb220180408134552.png)

2、选中先前创建好的证书，然后选择“创建自签名证书”。

![17.png](https://img1.jcloudcs.com/cms/3a6b1c28-a8af-4ee5-a4ba-ebee451c8c0b20180408134621.png)

3、设置一个简明知意的名称。

![18.png](https://img1.jcloudcs.com/cms/d839491d-8047-4436-8f8b-9ba0b523104f20180408134649.png)

**搭建https网站：**

1、新添加一个网站。

![19.png](https://img1.jcloudcs.com/cms/99497238-7f0f-4f0f-a8eb-3d9648913a3420180408135204.png)

2、设置好网站的主目录，设置类型为https，SSL证书选择前期设置好的testca即可。

![20.png](https://img1.jcloudcs.com/cms/21108999-47ae-4b27-a09e-206a8cfa314f20180408135228.png)

3、在网站根目录中设置一个Index.html的测试页面。

![25.png](https://img1.jcloudcs.com/cms/55d3a256-1337-4ddf-a64f-d34d0f49433a20180408135248.png)

4、选择站点，点击默认文档。

![21.png](https://img1.jcloudcs.com/cms/96ab240a-f9a4-4575-9f7d-a4e18fcbff3f20180408135305.png)

5、把Index.html默认文档上移到顶部。

![22.png](https://img1.jcloudcs.com/cms/e017c656-6b0a-4753-b756-211cf6c89ce720180408135415.png)

6、在外网使用HTTPS的方式做访问测试，可以看到可以访问，不过因为证书不是公共CA机构颁发的，所以会有安全提示，如果购买了CA证书，使用付费的证书，通常就不会有这个安全风险提示。

![23.png](https://img1.jcloudcs.com/cms/1ac8bf59-a95b-40d9-ab88-4e66ad9ed99d20180408135457.png)

7、选择“继续前往”可以看到网站能够正常访问。

![24.png](https://img1.jcloudcs.com/cms/a71fecd8-fe99-4ec5-ad76-0384a3f95b0d20180408135555.png)

如无法解决您的问题，请向我们提工单。