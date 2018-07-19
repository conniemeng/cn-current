### 1.前置依赖说明

使用京东云的文字识别 OCR服务前，用户需要在京东云对象存储服务上先创建一个空间bucket（如果已经有bucket，可使用现有bucket）。在调用OCR的API接口时，用户需要将该访问地址作为输入参数发起服务请求。该空间将用于存储被识别的图片（通过http上传或指定图片url方式提交的图片，都将存放在该bucket下再进行识别分析）。

在控制台访问对象存储服务，选择新建空间并获取该空间的外网访问域名，操作如下：

①先在控制台创建云存储空间

②获取云存储空间的外网访问域名，即为bucketDomain的值

### 2.通用文字识别

1.请求 URL

http://cognitive-console.jdcloud.com/service-ai/ocr/detect-text?appKey=[]&appName=[]&timestamp=[]&rand=[]&bucketDomain=[]

2.请求方式

POST

3.请求参数

1）Header参数
字段

说明Authorization

签名信息

2）Query参数(注意大小写敏感)

字段

说明appKey

用户appKey，可以从控制台获取appName

用户申请的appNametimestamp

当前时间戳bucketDomain

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.comrand

1-10000的随机数

3）Body参数

file文件

1.返回值
字段

类型

说明recognizeResult

JsonArray

检测结果httpCode

int

服务器错误码，200为成功msg

String

服务器返回信息timestamp

long

时间戳fileName

String

文件名称texts

array

识别出的文本列表area

object

文字行在图片中的坐标，图片左上角为坐标(0,0)text

String

识别出的文本文字errCode

int

文字识别服务返回的状态码errMsg

String

文字识别服务返回的状态信息

返回值示例：

{

"recognizeResult": [

{

"fileName": "TimLine图片20170601175137.jpg",

"texts": [

{

"area": {

"x": 126,

"width": 193,

"y": 137,

"height": 17

},

"text": "东半球最好用的手机"

}

],

"errCode": 0,

"errMsg": "成功"

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1497490835644

}

### 3.身份证识别

1.请求 URL

http://cognitive-console.jdcloud.com/service-ai/ocr/detect-idcard?appKey=[]&appName=[]&timestamp=[]&rand=[]&bucketDomain=[]

2.请求方式

POST

3.请求参数

1）Header参数
字段

说明Authorization

签名信息

2）Query参数(注意大小写敏感)

字段

说明appKey

用户appKey，可以从控制台获取appName

用户申请的appNametimestamp

当前时间戳bucketDomain

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.comrand

1-10000的随机数

3）Body参数

file文件

2.返回值
字段

类型

说明recognizeResult

JsonArray

检测结果httpCode

int

服务器错误码，200为成功msg

String

服务器返回信息timestamp

long

时间戳birthday

long

生日的时间戳fileName

String

文件名称address

String

地址gender

String

性别nationality

String

民族name

String

姓名id

String

身份证号errCode

int

文字识别服务返回的状态码errMsg

String

文字识别服务返回的状态信息

返回值示例：

{

"recognizeResult": [

{

"birthday": 632851200000,

"fileName":"sample.jpg",

"address": "福建省晋江市池店镇/*/*/*/*/*/*/*/*",

"gender": "男",

"nationality": "汉",

"errCode": 0,

"errMsg": "成功",

"name": "林/*/*",

"id":"35058219900121/*/*/*/*",

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1496643210608

}

### 4.银行卡识别

1.请求 URL

http://cognitive-console.jdcloud.com/service-ai/ocr/detect-bankcard?appKey=[]&appName=[]&timestamp=[]&rand=[]&bucketDomain=[]

2.请求方式

POST

3.请求参数

1）Header参数
字段

说明Authorization

签名信息

2）Query参数(注意大小写敏感)

字段

说明appKey

用户appKey，可以从控制台获取appName

用户申请的appNametimestamp

当前时间戳bucketDomain

用户京东云存储空间的外网访问域名,例如：

inf-dev-oss001.s-bj.jcloud.comrand

1-10000的随机数

3）Body参数

file文件

3.返回值
字段

类型

说明recognizeResult

JsonArray

检测结果httpCode

int

服务器错误码，200为成功msg

String

服务器返回信息timestamp

long

时间戳fileName

String

文件名称id

String

银行卡号errCode

int

文字识别服务返回的状态码errMsg

String

文字识别服务返回的状态信息

返回值示例：

{

"recognizeResult": [

{

"fileName": "sample.jpg",

"errCode": 0,

"errMsg": "成功",

"id":"622841031000039/*/*/*/*"

}

],

"httpCode": 200,

"msg": "请求成功",

"timestamp": 1496645820957

}