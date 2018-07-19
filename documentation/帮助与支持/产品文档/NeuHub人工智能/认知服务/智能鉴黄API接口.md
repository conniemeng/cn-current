开发者可通过指定图片URL地址、直接上传图片、指定对象存储图片地址这3种方式向调用智能鉴黄接口服务，接口描述如下：

调用接口1．指定图片URL地址的方式调用智能鉴黄接口

1.API接口说明

开发者可通过指定图片URL地址、直接上传图片、指定对象存储图片地址这3种方式向调用智能鉴黄接口服务，接口描述如下：

调用接口1．指定图片URL地址的方式调用智能鉴黄接口

请求 URL：

http://cognitive-console.jdcloud.com/service-ai/porn/oss/detect-url?appKey=[]&appName=[]&timestamp=[]&rand=[]

请求方式：

POST

请求参数：

请求包的http header
字段

说明Authorization

签名信息Content-Type

application/json

请求包的httpquery

Query参数

说明

是否必填appKey

用户的key

是appName

用户应用的名称

是timestamp

时间戳

是Rand

1-10000的随机数

是

请求包的http body

字段

类型

说明bucketDomain

String

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.comdata

List

需要识别图片URL的集合

例：{"bucketDomain":"inf-dev-oss001.s-bj.jcloud.com","data":["https://www.baidu.com/img/gaokao_pc_22894732028445b2e2caaf21ebc5e508.png"]}

返回内容：

返回类型：json

返回值：查看下表
字段

类型

说明detectResult

array

检测结果file

String

用户上传的图片文件名normalScore

double

正常指数，获取这几个指数的最大值，判断图片的类型hotScore

double

性感指数，获取这几个指数的最大值，判断图片的类型pronScore

double

色情指数，获取这几个指数的最大值，判断图片的类型errMsg

String

鉴黄服务返回的信息errCode

String

鉴黄服务返回的状态码

0成功

10000识别黄图失败

10001上传图片失败httpCode

int

服务器返回码:

200请求成功

207频繁操作

303登录失败

400请求参数出错

401没有登录

403没有权限

404找不到页面

408请求超时

409发生冲突

410已被删除

423已被锁定

500服务器出错msg

string

服务器返回信息timestamp

long

时间戳

****

请求示例（http请求）：

host:http://cognitive-console.jdcloud.com

url:/service-ai/porn/oss/detect-url?appKey=[appKey]&appname=[appName]&timestamp=[]&rand=[]

type：POST

Content-Type:"application/json"

Body：{"bucketDomain":"inf-dev-oss001.s-bj.jcloud.com","data":["https://www.baidu.com/img/gaokao_pc_22894732028445b2e2caaf21ebc5e508.png"]}

响应结果（application/json格式）：

{"detectResult":[

{

"file": "https://xdata.jcloud.com/resources/app/dataCloud/images/487x269-1.png",

"normalScore":0.9990476965904236,

"hotScore":0.000904505664948374,

"pornScore":0.000047795601858524606,

"errMsg": "ok"，

"errCode":"0"

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1495193951152

}}

调用接口2.直接上传图片方式调用智能鉴黄接口

请求 URL：

http://cognitive-console.jdcloud.com/service-ai/porn/oss/detect-upload?appKey=[]&appName=[]&timestamp=[]&rand=[]&bucketDomain=[]

请求方式：

POST

请求参数：

header
header参数

说明

是否必填Authorization

用户生成的签名

是

请求包的httpquery

Query参数

说明

是否必填appKey

用户的key

是appName

用户应用的名称

是Timestamp

时间戳

是bucketDomain

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.com

是rand

1-10000的随机数

是

请求包的http body

Body参数

说明

是否必填File

图片文件，支持批量一次最多（5张）

是

返回内容：

返回类型：json

返回值：
字段

类型

说明detectResult

array

检测结果file

String

用户上传的图片文件名normalScore

double

正常指数，获取这几个指数的最大值，判断图片的类型hotScore

double

性感指数，获取这几个指数的最大值，判断图片的类型pronScore

double

色情指数，获取这几个指数的最大值，判断图片的类型errCode

int

鉴黄服务返回的状态码errMsg

String

鉴黄服务返回的信息httpCode

int

服务器错误码，200为成功msg

String

服务器返回信息timestamp

long

时间戳

请求示例（http请求）：

host:http://cognitive-console.jdcloud.com

url:/service-ai/porn/oss/detect-upload?appKey=[appKey]&appName=[appName]&timestamp=[]&rand=[随机数]&bucketDomain=[用户京东云存储空间的外网访问域名]

type：POST

Body：sample.jpg

响应结果（application/json格式）：

{"detectResult":[

{

"file": "sample.jpg",

"normalScore":0.9990476965904236,

"hotScore": 0.000904505664948374,

"pornScore":0.000047795601858524606,

"errMsg": "ok"，

"errCode":"0"

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1495193951152

}}

调用接口3．指定图片对象存储地址的方式调用智能鉴黄接口

1.URL

http://cognitive-console.jdcloud.com/service-ai/porn/oss/detect-oss?appKey=[]&appName=[]&timestamp=[]&rand=[]

2.请求方式

POST

3.Header参数

字段

说明Authorization

签名信息Content-Type

application/json

4.Query参数(大小写敏感)

字段

说明appKey

用户appKey，可以从控制台获取appName

用户申请的appNametimestamp

当前时间戳rand

1-10000的随机数

5.Body参数

json字符串
字段

类型

说明bucketDomain

String

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.comdata

List

需要识别的图片所在的京东云存储路径的集合，例如：

["porn/2017-06-06/sample.jpg"]

例：{"bucketDomain":"inf-dev-oss001.s-bj.jcloud.com","data":["porn/2017-06-06/sample.jpg"]}

6.返回值

字段

类型

说明detectResult

JsonArray

检测结果httpCode

int

服务器错误码，200为成功msg

String

服务器返回信息timestamp

long

时间戳file

String

文件名称normalScore

double

正常指数，获取这几个指数的最大值，判断图片的类型hotScore

double

性感指数，获取这几个指数的最大值，判断图片的类型pornScore

double

色情指数，获取这几个指数的最大值，判断图片的类型errCode

int

文字识别服务返回的状态码errMsg

String

文字识别服务返回的状态信息

返回值示例：

{

"detectResult": [

{

"file": "sample.jpg",

"normalScore": 0.9998182654380798,

"hotScore":0.00016145552217494696,

"pornScore":0.000020341245544841513,

"errCode": 0,

"errMsg": "ok"

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1496820695879

}

限制条件说明:

直接上传图片方式调用智能鉴黄接口，一次接口请求文件大小不能超过10MB。