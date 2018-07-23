## **httpDNS**

## **什么是httpDNS?**

httpDNS是使用HTTP协议向DNS服务器80端口进行请求，代替传统的DNS协议53端口的DNS请求，绕开了运营商Local DNS的解析过程，从而避免了使用运营商Local DNS造成的域名劫持和跨网接入等问题。

##

![http.png](https://img1.jcloudcs.com/cms/8b4147fd-e272-42f5-a5a0-fb83a1d72f2620180301162629.png)

## ****

## **接口规范**

接口协议使用http 1.x，只支持GET方法，只支持在云解析接入的域名A记录的查询。

接口path: httpdns.jdgslb.com/v1/d

接口参数说明:

## 参数

含义dn

(必须) 要解析的域名，支持批量查询，以逗号分隔。ip

(可选)客户端ip(仅支持ipv4), 不填则由httpdns服务自动获取对端ip

参考示例如下：

http://httpdns.jdgslb.com/v1/d?dn=www.test.com&ip=202.108.7.3

返回为json格式，示例

成功返回示例：

{**"retCode"**:**0**,**"msg"**:**"ok"**,**"data"**:[
{
**"dn"**:**"**[www.test.com](http://www.test.com/)**"**,
**"type"**:**"A"**,
**"item"**:**"202.108.7.3"**,
**"ttl"**:**600**}
]}失败返回示例：

{**"retCode"**:**-1**,**"msg"**:**"failed reason: xxx"**,**"data"**:[]}