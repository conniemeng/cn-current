# **GetService(ListBuckets)**

对于服务地址作Get请求可以返回请求者拥有的所有Bucket，其中“/”表示根目录。

**请求语法**
GET / HTTP/1.1
Date: GMT Date
Authorization: SignatureValue
Host:s-bj.jcloud.com

**响应元素**

名称

描述Buckets

保存Bucket结果的集合

类型：List<Bucket>maxAge

Bucket的生命周期crrStatus

该Bucket下是否存在object在对外复制

类型:int:0(没有复制)或者1(存在复制)Name

Bucket名称。
类型：字符串CreationDate

Bucket创建时间

类型:时间(格式: "EEE, d MMM yyyy HH:mm:ss GMT")

Eg. Mon, 10 Jul 2017 08:49:15 GMTLocation

Bucket所在的数据中心

类型：字符串

目前返回空字符串””

细节分析

1. GetService这个API只对验证通过的用户有效。

2. 如果请求中没有用户验证信息（即匿名访问），返回403 Forbidden。错误码：AccessDenied。

**请求示例**
GET / HTTP/1.1
Date: Wed, 12 Jul 2017 10:38:35 GMT
Authorization: jingdong 298718BEDE59FF1B2E96A3152937D37B:mIdihnpi2ZtWTHaji555S0BBEBA=
Host: s-bj.jcloud.com
Connection: Keep-Alive

**返回示例**

HTTP/1.1 200 OK
Server: nginx
Date: Wed, 12 Jul 2017 10:38:35 GMT
Content-Type: application/json;charset=UTF-8
Content-Length: 462
Connection: keep-alive
x-jss-request-id: A2FC27C60E0BC115
{"Buckets":[{"maxAge":0,"crrStatus":0,"Name":"oss-test-cn-north-1",
"CreationDate":"Mon, 10 Jul 2017 08:49:15 GMT","Location":""},
{"maxAge":0,"crrStatus":0,"Name":"sanitytest-object-hb","CreationDate":"Mon,
10 Jul 2017 13:47:57 GMT","Location":""},
{"maxAge":0,"crrStatus":0,"Name":"video-test","CreationDate":"Tue, 11 Jul 2017 10:03:07 GMT","Location":""},
{"maxAge":0,"crrStatus":0,"Name":"oss-test","CreationDate":"Wed, 12 Jul 2017 07:40:46 GMT","Location":""}]}