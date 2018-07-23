# 负载均衡开启获取真实IP后nginx配置

负载均衡使用四层协议透传模式监听TCP80端口后，如果打开获取真实IP选项，如图所示：

![nginx1.JPG](https://img1.jcloudcs.com/cms/c6f30da4-6549-4a4d-aa6c-3e922b12254220180201194758.JPG)

访问nginx网页会出现400错误，无法访问网页。此时需要修改nginx网页的配置文件，添加反向代理协议的监听，以默认页面举例，编辑/etc/nginx/conf.d/default.conf，在如图所示的位置添加“proxy_protocal”内容

![nginx2.JPG](https://img1.jcloudcs.com/cms/b880433a-30c8-4991-8589-901575570c6220180201195153.JPG)

保存文件后重启nginx服务。通过负载均衡IP公网访问nginx网页可以正常显示内容。