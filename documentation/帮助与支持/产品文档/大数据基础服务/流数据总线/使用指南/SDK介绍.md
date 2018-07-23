流数据总线支持用户通过SDK的方式进行数据的写入与读取，暂时仅支持JAVA语言SDK，具体使用方法如下：

**1.****下载SDK**

[](https://xdata.jcloud.com/map/spsdownload/downLoadJavaSDK.action)

[https://xdata.jdcloud.com/map/spsdownload/downLoadJavaSDK.action](https://xdata.jdcloud.com/map/spsdownload/downLoadJavaSDK.action)

**2.****安装SDK**

请将下载的压缩文件解压，然后将jar包引入项目中，参照如下的DEMO程序进行开发。

**3.****数据写入**

（1）StreamHubUpload

创建StreamHubUpload有两种方式，异步调用方式和自定义调用方式。

l**异步调用方式**

参数说明：

accessKey : your access key

secretKey: your secret key

topicName:上传数据对应的主题名称

StreamHubUpload(String accessKey, StringsecretKey, String topicName)

l**自定义调用方式**

参数说明：

accessKey : your access key

secretKey: your secret key

topicName:上传数据对应的主题名称

asynchronousfalse : true :

StreamHubUpload(String accessKey, StringsecretKey, String topicName, Boolean asynchronous )

代码样例：
String endpoint = "http://streamhub-gw.jcloud.com";

String accessKey = "Your AccessKey";

String accessScrect = "Your AccessScrect";

String topicName = " Your TopicName";

StreamHubUpload streamingHubUpload = **new** StreamHubUpload(accessKey, accessScrect, topicName, endpoint);

（2）创建上传数据对象

String msg = "单条消息";

Entity entity = **new** Entity();

entity.setKey("KEY：");

entity.setValue("VALUE："+ msg);

（3）调用上传方法

流式处理提供单条上传和多条上传两种数据写入方式。

l**单条上传**

单独的记录写入数据流有两个方法:

指定分区上传方法 :putStreamRecord( Entity, Partition)

未指定分区上传方法 :putStreamRecoredNoPartiton(Entity)

l**多条上传**

批量记录写入数据流有两个方法:

指定分区上传方法 :putStreamRecords(List, Partition )

未指定分区上传方法 :putStreamRecordsNoPartiton(List)
String msg = "单条消息";

Entity entity = **new** Entity();

entity.setKey("KEY：");

entity.setValue("VALUE："+ msg);

String recordId = streamingHubUpload.putStreamRecord(entity, 1);

System.*out*.println("upload data result : " + recordId);

List entities = **new** ArrayList();

Entity entity1 = **null**;

**for**(**int** i = 0; i < 10; i++) {

entity1 = **new** Entity();

entity1.setKey("批量消息KEY:"+ i);

entity1.setValue("批量消息VALUE:"+ i);

entities.add(entity1);

}

String recordIds = streamingHubUpload.putStreamRecords(entities, 1);

System.*out*.println("upload data result : " + recordIds);

（4）返回结果说明
参数

参数说明result

true :上传成功 | false : 上传失败message

上传返回信息code

上传信息码

****

**4.****数据读取**

（1）创建StreamHubFetch

参数说明：

accessKey : your access key

secretKey: your secret key

topicName:写入数据对应的主题名称

StreamHubFetch(String accessKey,String secretKey, String topicName)

代码样例：
String endpoint = "http://streamhub-gw.jcloud.com";

String accessKey = "Your AccessKey";

String accessScrect = "Your AccessScrect";

String topicName = " Your TopicName";

StreamHubFetch streamHubFetch = **new** StreamHubFetch(accessKey, accessScrect, topicNam

（2）调用读取方法

参数说明：

partition :分区值，用于说明从指定的分区读取数据

offset:偏移量，用于说明读取的起始位置

数据读取方法 :fetchStreamRecord( partition, offset)
StreamHubFetch streamHubFetch = **new** StreamHubFetch(accessKey, accessScrect, topicName, endpoint);

String result = streamHubFetch.fetchStreamRecord(1, 1);

System.*out*.println("fetch result = ");

System.*out*.println(result);

（3）返回结果说明
参数

参数说明Result

true :读取成功 | false : 读取失败Message

读取数据返回的提示信息Code

系统返回状态码，详细情况见状态码说明部分data

其中有两个字段，total字段表示此次读取操作获取的数据条数，data字段对应的为一个JsonArray，顺序存储了读取出的数据