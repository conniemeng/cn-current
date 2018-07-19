# **GetBucket(ListObject)**

此操作用于列出指定Bucket中所有的Object信息。

注意：即使Bucket的访问权限为public，也不允许匿名使用此操作，需要指定Authorization。

### **请求语法**

GET / HTTP/1.1
Host: BucketName. s.jcloud.com
Date: GMT Date
Authorization: signatureValue/#请参照“访问控制”

**请求参数**

ListObject时可以通过prefix，marker，delimiter和maxKeys对list做限定，返回部分结果。
名称

描述delimiter

是一个用于对Object名字进行分组的字符。所有名字包含指定的前缀且第一次出现delimiter字符之间的object作为一组元素——CommonPrefixes。

数据类型：字符串
默认值：无marker

返回以字典序排序的Object信息的起始标志，结果中不包含marker
数据类型：字符串
默认值：无maxKeys

限定此次返回object的最大数，如果不设定，默认为1000
数据类型：字符串
默认值：1000prefix

限定返回的object key必须以prefix作为前缀。注意使用prefix查询时，返回的key中仍会包含prefix。
数据类型：字符串
默认值：无

### **响应元素**

名称

描述Name

Bucket名字
类型：字符串Prefix

本次查询结果的开始前缀。
类型：字符串Marker

标明这次List Object的起点。
类型：字符串NextMarker下一次List Object的起点。
类型：字符串Delimiter

是一个用于对Object名字进行分组的字符。所有名字包含指定的前缀且第一次出现delimiter字符之间的object作为一组元素--CommonPrefixes。
类型：字符串MaxKeys

响应请求内返回结果的最大数目。
类型：intHasNext

指明是否所有的结果都已经返回； “true”表示本次没有返回全部结果；“false”表示本次已经返回了全部结果。
类型：布尔型
有效值：true、falseContents

保存每个返回Object meta的集合。
类型：ListKey

Object的Key.
类型：字符串ETag

ETag 是京东云存储中Object的Hash值，其仅反映Object的数据内容，而不包括元数据(Metadata)。需要注意的是ETag并不一定是一个MD5值，当PUT Object操作完成时，服务端会为收到的数据生成MD5 摘要作为其ETag。而对于Multipart Upload产生的Object， 其ETag并不是内容的ContentMD5
类型：字符串LastModified

Object最后被修改的时间。
类型：字符串Size

Object的字节数。
类型：LongStorageClass

Object的存储类型，支持“STANDARD”（标准存储），“REDUCED_REDUNDANCY”（低频访问型）（注意，目前“REDUCED_REDUNDANCY”仅华北机房支持）
类型：字符串CommonPrefixes

标明那些以delimiter结尾，并有共同前缀的object名称的集合。
类型：List

细节分析

1. 如果访问的Bucket不存在，包括试图访问因为命名不规范无法创建的Bucket，返回404 Not Found错误，错误码：NoSuchBucket。

2. 如果没有访问该Bucket的权限，返回403 Forbidden错误，错误码：AccessDenied。

3. 在做条件查询时，即使marker实际在列表中不存在，返回也从符合marker字母排序的下一个开始打印。如果max-keys小于0或者大于1000，max-keys被自动设置成默认值1000。

4. 如果把prefix设为某个文件夹名，就可以罗列以此prefix开头的文件，即该文件夹下递归的所有的文件和子文件夹。如果再把delimiter设置为 / 时, 返回中 Contents下只罗列该文件夹的文件，而CommonPrefixes下则会罗列该文件夹的子文件夹名称部分，子文件夹下递归的文件和文件夹不被显示。如一个bucket存在三个object ：jingdong/test.jpg，jingdong/dir/file，jingdong/dir/file2。若设定prefix为”jingdong/” ，则返回三个object；如果增加设定delimiter为“/”，则Contents中返回文件 ”jingdong/test.jpg”和 CommonPrefixes 中返回文件夹”jingdong/dir”；即实现了文件夹的逻辑。

5. marker 为以字典序排序的 Object 信息的起始标志，结果中不包含 marker，可以设定marker 为本次列表最后一个 Key，来获取其他的本次操作未返回的 Object 信息，通常与 maxKeys 一起使用来实现分页

### **请求示例**

GET / HTTP/1.1
Host: oss-example.s-bj.jcloud.com
Date: Tue, 11 Jul 2017 07:54:41 GMT
Authorization: jingdong qbS5QXpLORrvdrmb:3xo8IxIXSkA280C0Z5+lkowaAA8=

**返回示例**

HTTP/1.1 200 OK
Server: nginx
Date: Tue, 11 Jul 2017 07:54:41 GMT
Content-Type: application/json;charset=UTF-8
Content-Length: 900
Connection: keep-alive
Vary: Accept-Encoding
Vary: Accept-Encoding
x-jss-request-id: 99D8C1866CAC92D0
X-Trace: 200-1499759681772-0-0-19-42-42
{
"Name": "oss-example",
"Prefix": null,
"Marker": null,
"NextMarker":null,
"Delimiter": null,
"MaxKeys": 1000,
"HasNext": false,
"HasCommonPrefix": true,
"Contents": [
{
"Key": "jingdong/dir/file",
"LastModified": "Mon, 17 Jul 2017 12:12:39 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
},
{
"Key": "jingdong/dir/file2",
"LastModified": "Mon, 17 Jul 2017 12:14:49 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
},
{
"Key": "jingdong/test.jpg",
"LastModified": "Mon, 17 Jul 2017 12:12:17 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
},
{
"Key": "test.jpg",
"LastModified": "Mon, 17 Jul 2017 12:11:56 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
}
],
"CommonPrefixes": [ ]
}

**请求示例(含Prefix参数)**

GET /?prefix=jingdong%2F HTTP/1.1
Host: oss-example.s-bj.jcloud.com
Date: Tue, 11 Jul 2017 08:01:09 GMT
Authorization: jingdong qbS5QXpLORrvdrmb:FQZNWlNAraOLgreEflrurbNojJE=

**返回示例(含Prefix参数)**

HTTP/1.1 200 OK
Server: nginx
Date: Tue, 11 Jul 2017 08:01:09 GMT
Content-Type: application/json;charset=UTF-8
Content-Length: 613
Connection: keep-alive
Vary: Accept-Encoding
Vary: Accept-Encoding
x-jss-request-id: 9CCEA5403AA5ED6E
X-Trace: 200-1499760069435-0-0-20-45-45
{
"Name": "oss-example",
"Prefix": "jingdong/",
"Marker": null,
"NextMarker":null,
"Delimiter": null,
"MaxKeys": 1000,
"HasNext": false,
"HasCommonPrefix": true,
"Contents": [
{
"Key": "jingdong/dir/file",
"LastModified": "Mon, 17 Jul 2017 12:12:39 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
},
{
"Key": "jingdong/dir/file2",
"LastModified": "Mon, 17 Jul 2017 12:14:49 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
},
{
"Key": "jingdong/test.jpg",
"LastModified": "Mon, 17 Jul 2017 12:12:17 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
}
],
"CommonPrefixes": [ ]
}

**请求示例(含prefix和delimiter参数)**

GET /?prefix=jingdong%2F&delimiter=%2F HTTP/1.1
Host: oss-example.s-bj.jcloud.com
Date: Tue, 11 Jul 2017 08:05:13 GMT
Authorization: jingdong qbS5QXpLORrvdrmb:jXw8QQvs6IS+JJ2EpiFMUGtgNEM=

**返回示例(含prefix和delimiter参数)**

HTTP/1.1 200 OK
Server: nginx
Date: Tue, 11 Jul 2017 08:05:13 GMT
Content-Type: application/json;charset=UTF-8
Content-Length: 456
Connection: keep-alive
Vary: Accept-Encoding
Vary: Accept-Encoding
x-jss-request-id: 96F2C2E9FC9B3BE5
X-Trace: 200-1499760313279-0-0-20-45-45
{
"Name": "oss-example",
"Prefix": "jingdong/",
"Marker": null,
"NextMarker":null,
"Delimiter": "/",
"MaxKeys": 1000,
"HasNext": false,
"HasCommonPrefix": false,
"Contents": [
{
"Key": "jingdong/test.jpg",
"LastModified": "Mon, 17 Jul 2017 12:12:17 GMT",
"ETag": "77abd5a162ef88440102129fffbb404c",
"Size": 2884006,
"StorageClass": "STANDARD"
}
],
"CommonPrefixes": [
"jingdong/dir"
]
}