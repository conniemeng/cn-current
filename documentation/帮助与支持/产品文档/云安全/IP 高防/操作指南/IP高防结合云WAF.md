# **IP高防结合云WAF**

京东云“IP高防”和“Web应用防火墙”能够完美兼容。将WAF的域名接入高防后，流量会先过高防再到WAF。流程示意如下：

**访问流量–> IP高防–>WAF–>用户源站。**

## **配置步骤如下：**

1、在控制台，云安全下找到Web应用防火墙，进入“网站配置”页面。

![WAF.jpg](https://img1.jcloudcs.com/cms/a1b0988b-1108-44a6-bf47-78a45e657eed20180706113641.jpg)

在操作栏中，选择“编辑”按钮，然后如下图所示，开启代理。

![123.jpg](https://img1.jcloudcs.com/cms/69aee980-4a5b-4fae-8b9b-bcc80c9afd0720180705185414.jpg)

2、配置“IP高防”

在网站类转发规则中，回源方式，选择回源域名。填写刚才Web应用防火墙生成的cname。

![323.jpg](https://img1.jcloudcs.com/cms/03997464-1c7d-46c9-b878-02b5bbbdee4c20180705185607.jpg)

3、变更DNS解析

将域名解析指向DDoS高防生成的CNAME地址。实现网站流量先经过DDoS高防，再转发到Web应用防火墙。请参考：[修改DNS解析](https://www.jdcloud.com/help/detail/2275/isCatalog/1 "修改DNS解析")