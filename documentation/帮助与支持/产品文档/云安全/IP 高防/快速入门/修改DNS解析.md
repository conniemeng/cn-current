# 修改DNS解析

1、找到IP高防的cname

在“实例列表”页面，进入转发规则，复制待修改的cname值。

以非网站转发规则为例，如下找到红框处待复制的cname：

![修改DNS解析1.png](https://img1.jcloudcs.com/cms/a562b53b-fe81-4bd7-af9e-e0b7c7dc795a20180322111309.png)

2、在域名提供商处，需要修改域名解析配置让域名解析到高防IP上。红框处，填写刚才复制的cname信息。

以京东云“云解析”为例，在控制台–》“域名服务”–》“云解析”，进入京东云解析的页面。

![云解析边栏.png](https://img1.jcloudcs.com/cms/ed023c47-ff86-41d6-894d-8d9a0fde020120180322111428.png)

找到待解析的域名，如下：

![修改DNS解析2.png](https://img1.jcloudcs.com/cms/1566abef-ace4-4fec-a6e3-6db96535f55420180322111605.png)

单击进入解析配置：

![DNS解析2.png](https://img1.jcloudcs.com/cms/b2821e5d-62e9-4f56-9232-ea9ad350f06320180322111528.png)

将记录值，改为IP高防的cname地址即可。