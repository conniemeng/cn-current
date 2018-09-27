### 接口描述

提供中文分词、词性标注、命名实体识别三个功能，解析自然语言中的基本语言元素，并赋予词性，进一步将文本中的特定类型的事物名称或符号识别。

### 调用方式

**HTTP****接口**

****

请求报文：

GET /nlp/lexer?token=<token>&appId=<appId>&text=<text>&type=<type>

Host: ai-api.jd.com

Token: 94d9476f-bd7-43c7-836d-b1f1015e6b7

**请求参数：**

入参:

参数名

类型

说明token

string

API的调用方标识，从AI平台获取。appId

string

应用id，同一调用方可以创建多个应用，appId为0时表示使用通用的分词模型。text

string

输入文本type

int

选择所需的词法分析的结果，包括"分词"、"词性标注"和"命名实体识别”一个或多个的组合。 0: 提供分词，词性标注以及命名实体识别的结果 1: 提供分词的结果 2: 提供分词和词性标注的结果 3: 提供分词和命名实体的结果

响应报文：

头部信息

头部名称

必填

说明content-Type

是

正常情况下该值将被设为application/json，表示返回JSON格式的文本信息。

响应状态码
HTTP状态码

含义200

获取响应成功信息

响应内容： 如果请求成功，返回包含下内容的JSON字符串（已格式化，便于阅读<克林顿访问中国 >）：

{

"status": 0, //状态码，0表示正常识别

"request_id": "xxxxx", //本次请求服务端所分配的id

"text": "克林顿访问中国" //输入文本原句

//分词结果列表。

"tokenizedText": [

{

"word": "克林顿", //分词

"pos": "NR", //词性

"ner": "PERSON", //命名实体识别

"offset": 0, //距离起始位置偏移

"length": 3 //分词长度

},

{

"word": "访问",

"pos": "VV",

"ner": "O",

"offset": 3,

"length": 2

},

{

"word": "中国",

"pos": "NR",

"ner": "GPE",

"offset": 5,

"length": 2

}

]

}

### 示例代码

### HTTP接口

http://ai-api.jd.com/nlp/lexer?token=94d9476f-0bd7-43c7-836d-b1f10151e6b7&appId=0&text=克林顿访问中国&type=0

**Hadoop****上使用**

Hive UDF
Example.hqlset mapreduce.map.memory.mb=20480; set mapreduce.reduce.memory.mb=20480; set mapreduce.map.java.opts=-Xmx20480m; set mapreduce.reduce.java.opts=-Xmx20480m; ADD JAR hdfs:///user/mart_tbi/zhenting/udf_jar/jd-nlu-models-chinese-3.6.1-SNAPSHOT.jar; ADD JAR hdfs:///user/mart_tbi/zhenting/udf_jar/jd-nlu-ner-models-chinese-3.6.0-SNAPSHOT.jar; ADD JAR hdfs:///user/mart_tbi/zhenting/udf_jar/fairy-offline-0.1-SNAPSHOT-jar-with-dependencies.jar; ADD JAR hdfs:///user/mart_tbi/zhenting/udf_jar/fairy-udf-0.1.jar; ADD ARCHIVE hdfs:///user/mart_tbi/zhenting/fairy_root//lexeme/zhangzhenting3/12/udf_data.zip; CREATE TEMPORARY FUNCTION lexeme as 'com.jd.fairy.hadoop.udf.hive.LexemeUDF'; select count(lexeme(text, '12', '470670c2-3dcd-487d-b424-c3ab6917c435', 'hdfs:///user/mart_tbi/zhenting/fairy_root/').words) from app.seg_test;run.shexport JAVA_HOME=/software/servers/jdk1.8.0_121 export HADOOP_CLIENT_OPTS="$HADOOP_CLIENT_OPTS -Xmx20480m" hive -f example.hql

pig UDF
example.pigREGISTER hdfs:///user/mart_tbi/zhenting/udf_jar/jd-nlu-models-chinese-3.6.1-SNAPSHOT.jar;

REGISTER hdfs:///user/mart_tbi/zhenting/udf_jar/jd-nlu-ner-models-chinese-3.6.0-SNAPSHOT.jar;

REGISTER hdfs:///user/mart_tbi/zhenting/udf_jar/fairy-offline-0.1-SNAPSHOT-jar-with-dependencies.jar;

REGISTER hdfs:///user/mart_tbi/zhenting/udf_jar/fairy-udf-0.1.jar;

DEFINE LEXEME com.jd.fairy.hadoop.udf.pig.LexemeUDF('470670c2-3dcd-487d-b424-c3ab6917c435','12','hdfs:///user/mart_tbi/zhenting/fairy_root/');

raw_data = LOAD 'app.seg_test'

USING org.apache.hive.hcatalog.pig.HCatLoader();

data = FOREACH raw_data

GENERATE LEXEME(text);

dump data;run.sh/#!/usr/bin/env bash

set -x

set -e

export JAVA_HOME=/software/servers/jdk1.8.0_121

pig \

-useHCatalog \

-Dmapreduce.job.acl-view-job=/* \

-Dmapreduce.job.queuename=root.bdp_jmart_tbi_union.bdp_jmart_tbi_dev \

-Dmapred.create.symlink=yes \

-Dmapreduce.map.java.opts='-Xmx20480m ' \

-Dmapreduce.map.memory.mb=20480 \

-Dmapreduce.reduce.memory.mb=20480 \

lexeme.pig