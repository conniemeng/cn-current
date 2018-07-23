# DBUS使用说明文档

## SDK下载

您可以通过以下地址下载最新版本的SDK，下载：[//xdata.jcloud.com/map/spsdownload/downLoadJavaSDK.action](http://xdata.jcloud.com/map/spsdownload/downLoadJavaSDK.action)

## SDK安装

请将下载的压缩文件解压，然后将两个jar包引入项目中，然后参照如下的DEMO程序进行开发，实现数据上传。

## DBUS上传数据

### 上传数据流程

1.创建 TransportTable

2.创建 UploadSession

3.RecordWriter, Record

4.提交上传操作

### 接口

创建uploadSession创建上传接口

transport= new TableTransport(appKey,secretKey)

//设置上传数据通道

//END_POINT_HTTP:外网地址(默认传输通道)

//END_POINT_HTTPS:外网安全通道(数据加密,但会减低上传速度)

//END_POINT_LOCAL:内网通道(京东云内网通道)

//transport.setEndpoint(TableTransport.END_POINT_HTTP);//默认设置在非分区表上创建上传会话

public TableTransport.UploadSession createUploadSession(String db, String tableName)在分区表上创建上传会话

public TableTransport.UploadSession createUploadSession(String db, String tableName, PartitionSpec partitionSpec)

打开文件上传Writer打开文件writer

//*/*

/*打开{@link com.jcloud.bds.data.RecordWriter}用来写入数据

/*

/* BlockId是由用户选取的0~19999之间的数值，标识本次上传数据块

/*

/* @param blockId

/*块标识

/*/

public RecordWriter openRecordWriter(long blockId)打开文件writer

//*/*

/*打开{@link RecordWriter}用来写入数据

/*

/* @param blockId

/*块标识

/* @param compress

/*数据传输是否进行压缩

/*/

public RecordWriter openRecordWriter(long blockId, boolean compress)打开文件writer

//*/*

/*打开{@link RecordWriter}用来写入数据

/*

/* @param blockId

/*块标识

/* @param compress

/*数据传输是否进行压缩

/*/

public RecordWriter openRecordWriter(long blockId, CompressOption compress)

提交上传提交块列表

//*/*

/*提交本次上传的所有数据块

/*

/*

/* blcoks表示用户记录的已经成功上传的数据块列表，用来与服务器端做完整性校验

/*

/*

/* @param blocks

/*用户预期已经上传成功的数据块列表

/* @throws TransportException

/*如果提供的Block列表与Server端存在的Block不一致抛出异常

/* @throws IOException

/*/

public void commit(Long[] blocks)

### 上传demo

[]()[**import**]()****java.io.IOException;
**import**java.io.UnsupportedEncodingException;
**import**java.util.ArrayList;
**import**java.util.Iterator;
**import**java.util.List;
*//*/*
/* Created by guihuawen on 16-1-14.
/*/***public class**DownloadDemo {
**private static**String*accessID*=**"<your access id>"**;
**private static**String*accessKey*=**"<your access key>"**;
**private**String**end_point**=**"http://bds-api.jcloud.com"**;
**private static**String*db*=**"<your db>"**;
**private static**String*table*=**"<your table>"**;
**private**String**partitonSpecLiteral**=**"<your partition>"**;*//dt=2009-12-09/hour=02***private**BDS**bds**;
**private**TableTransport**transport**;
**public static void**main(String[] args)**throws**IOException, BdsException {
**new**DownloadDemo().download();
}
**public void**download()**throws**IOException, BdsException {
*//**根据用户context初始化bds实例*Account account =**new**BdsAccount(*accessID*,*accessKey*);
**bds**=**new**BDS(account);
**bds**.setEndpoint(**end_point**);
**transport**=**new**TableTransport(**bds**);
*//**获取表分区信息*TableService tableService =**new**TableService(**bds**);
ShowCreateTable showCreateTable = tableService.descTable(*db*,*table*);
**boolean**isPartitioned = showCreateTable.isPartitioned();
**if**(!isPartitioned) {
*//**非分区表***if**(**partitonSpecLiteral**!=**null**) {
**throw new**BdsException(**"ERROR: can not specify partition for an unpartitioned table"**);
}
*//**对整张表进行分片下载***this**.splitTableByThreads((PartitionSpec)**null**);
}**else**{
*//**分区表
//获取分区列表 startTime:{dt='2015-11-27',dt='2015-11-28',dt='2015-11-29'}*List partitions=**this**.inferPartitionSpecs(**partitonSpecLiteral**,account,showCreateTable);
**if**(partitions.size() ==0) {
**throw new**BdsException(**"ERROR: can not infer any partitions from: "**+**this**.**partitonSpecLiteral**);
}
**if**(partitions.size() ==1) {
*//**只有一个分区*PartitionSpec sliceId = (PartitionSpec)partitions.get(0);
**this**.splitTableByThreads(sliceId);
}**else**{
*//**下载分区表多个分区数据,一个分区的数据对应一个下载session***for**(Iterator i$ = partitions.iterator(); i$.hasNext();) {
PartitionSpec ps = (PartitionSpec)i$.next();
*//**初始化下载session*TableTransport.DownloadSession downloadSession=**transport**.createDownloadSession(*db*,*table*,ps);
List<Column> columns=downloadSession.getSchema().getColumns();
**int**blockSize=downloadSession.getSplitSize();
**for**(**int**blockId=0;blockId<blockSize;blockId++){
RecordReader recordReader = downloadSession.openRecordReader(blockId);
Record record;
**while**((record = recordReader.read()) !=**null**){
System.***out***.println(formatString(record,columns));
*//****TODO parse record to your case***}
recordReader.close();
}
}
}
}
System.***err***.println(**"download OK"**);
}
*//**无分区表或下载单分区数据, 使用同一个session,启动多个线程下载***private void**splitTableByThreads(PartitionSpec ps)**throws**IOException, TransportException {
TableTransport.DownloadSession downloadSession;
**if**(ps ==**null**) {
downloadSession =**transport**.createDownloadSession(*db*,*table*);
}**else**{
downloadSession =**transport**.createDownloadSession(*db*,*table*, ps);
}
*//**下载分片数***int**blockSize = downloadSession.getSplitSize();
**for**(**int**blockId =0; blockId < blockSize; blockId++) {
RecordReader recordReader = downloadSession.openRecordReader(blockId);
Record record;
List<Column> columns=downloadSession.getSchema().getColumns();
**while**((record = recordReader.read()) !=**null**){
System.***out***.println(formatString(record,columns));
*//****TODO parse record to your case***}
recordReader.close();
}
}
**public**List<PartitionSpec> inferPartitionSpecs(String partitionSpecLiteral,Account account,ShowCreateTable showCreateTable)**throws**BdsException {
List<PartitionSpec> partitionSpecList=**new**ArrayList<PartitionSpec>();
**if**(partitionSpecLiteral==**null**){
ShowPartitionModel partitions = showCreateTable.getShowPartitionModel();
**if**(partitions!=**null**){
partitionSpecList=partitions.getPartitionSpecs();
}
}**else**{
partitionSpecList=**new**PartitionSpec().parsePartitionSpecList(partitionSpecLiteral);
}
**return**partitionSpecList;
}
**public**String formatString(Record r,List<Column> columns)**throws**UnsupportedEncodingException {
StringBuffer line=**new**StringBuffer();
**int**cols =columns.size();
**for**(**int**i =0; i < cols; ++i) {
*//BIGINT, DOUBLE, BOOLEAN, DATETIME, STRING, DECIMAL, MAP, ARRAY;*DataType type = columns.get(i).getType();
String v;
**switch**(type){
**case*****BIGINT***:
line.append(r.getBigint(i));
**break**;
**case*****DOUBLE***:
line.append(r.getDouble(i));
**break**;
**case*****BOOLEAN***:
line.append(r.getBoolean(i));
**break**;
**case*****DATETIME***:
line.append(r.getDatetime(i));
**break**;
**case*****STRING***:
line.append(r.getString(i));
**break**;
**case*****DECIMAL***:
line.append(r.getDecimal(i));
**break**;
**default**:
**throw new**RuntimeException(**"Unknown column type: "**+ type);
}
**if**(i<cols-1){
line.append(**","**);
}
}
**return**line.toString();
}
}

## DBUS下载数据

### 下载数据流程

1.创建 TransportTable

2.创建 DownloadSession

3.RecordReader, Record

### 接口

创建downloadSession创建下载接口

TableTransport transport = new TableTransport(appKey, secretKey)

//设置上传数据通道

//END_POINT_HTTP:外网地址(默认传输通道)

//END_POINT_HTTPS:外网安全通道(数据加密,但会减低上传速度)

//END_POINT_LOCAL:内网通道(京东云内网通道)

//transport.setEndpoint(TableTransport.END_POINT_HTTP);//默认设置在非分区表上创建下载会话

/* @param db

/* database名

/* @param tableName

/*表名，非视图

/* @param partitionSpec

/*指定分区 {@link PartitionSpec}

createDownloadSession(String db, String tableName)在分区表上创建下载会话

/* @param db

/* database名

/* @param tableName

/*表名，非视图

createDownloadSession(String db, String tableName,PartitionSpec partitionSpec)

打开文件下载Reader打开文件读取器

/* @param splitNum

/*本次要读取记录的分片编号

openRecordReader(int splitNum)打开文件读取器

/* @param splitNum

/*本次要读取记录的分片编号

/* @param compress

/*数据传输是否进行压缩；即使设置了压缩选项，如果server 不支持压缩，传输数据也不会被压缩

openRecordReader(int splitNum, boolean compress)打开文件读取器

/* @param splitNum

/*本次要读取记录的分片编号

/* @param compress

/*数据传输是否进行压缩；即使设置了压缩选项，如果server 不支持压缩，传输数据也不会被压缩

openRecordReader(int splitNum, CompressOption compress)打开文件读取器

/* @param splitNum

/*本次要读取记录的分片编号

/* @param compress

/*数据传输是否进行压缩；即使设置了压缩选项，如果server 不支持压缩，传输数据也不会被压缩

/* @param columns

/*本次需要下载的列

openRecordReader(int splitNum, boolean compress,List

### 下载demo

**package****import****import**java.io.IOException;
**import**java.io.UnsupportedEncodingException;
**import**java.util.ArrayList;
**import**java.util.Iterator;
**import***//*/*
/* Created by guihuawen on 16-1-14.
/*/***public class**DownloadDemo {
**private static**String*accessID*=**"**;
**private static**String*accessKey*=**"**;
**private**String**end_point**=**"http://dbus.jcloud.com"**;
**private static**String*db*=**"**;
**private static**String*table*=**"**;
**private**String**partitonSpecLiteral**=**"**;*//dt=2009-12-09/hour=02***private**BDS**bds**;
**private**TableTransport**transport****public static void**main(String[] args)**throws**IOException, BdsException {
**new****public void**download()**throws**IOException, BdsException {
*//**根据用户context初始化bds实例*Account account =**new**BdsAccount(*accessID*,*accessKey*);
**bds**=**new**BDS(account);
**bds**.setEndpoint(**end_point**);
**transport**=**new**TableTransport(**bds**);
*//**获取表分区信息*TableService tableService =**new**TableService(**bds**);
ShowCreateTable showCreateTable =tableService.descTable(*db*,*table*);
**boolean**isPartitioned =showCreateTable.isPartitioned();
**if**(!isPartitioned) {
*//**非分区表***if**(**partitonSpecLiteral**!=**null**) {
**throw new**BdsException(**"ERROR: can not specify partition foran unpartitioned table"***//**对整张表进行分片下载***this**.splitTableByThreads((PartitionSpec)**null**);
}**else**{
*//**分区表
//获取分区列表 startTime:{dt='2015-11-27',dt='2015-11-28',dt='2015-11-29'}*List partitions=**this**.inferPartitionSpecs(**partitonSpecLiteral**,account,showCreateTable);
**if**(partitions.size() ==0) {
**throw new**BdsException(**"ERROR: can not infer any partitionsfrom: "**+**this**.**partitonSpecLiteral****if**(partitions.size() ==1) {
*//**只有一个分区*PartitionSpec sliceId = (PartitionSpec)partitions.get(0);
**this**.splitTableByThreads(sliceId);
}**else**{
*//**下载分区表多个分区数据,一个分区的数据对应一个下载session***for***//**初始化下载session*TableTransport.DownloadSessiondownloadSession=**transport**.createDownloadSession(*db*,*table***int**blockSize=downloadSession.getSplitSize();
**for**(**int**blockId=0**while**((record = recordReader.read()) !=**null**){
System.***out***.println(formatString(record,columns));
*//****TODO parse record to your case******err***.println(**"download OK"***//**无分区表或下载单分区数据, 使用同一个session,启动多个线程下载***private void**splitTableByThreads(PartitionSpec ps)**throws****if**(ps ==**null**) {
downloadSession =**transport**.createDownloadSession(*db*,*table*);
}**else**{
downloadSession =**transport**.createDownloadSession(*db*,*table**//**下载分片数***int**blockSize =downloadSession.getSplitSize();
**for**(**int**blockId =0**while**((record = recordReader.read()) !=**null**){
System.***out***.println(formatString(record,columns));
*//****TODO parse record to your case*****public**List**throws**BdsException {
List**new**ArrayList**if***isEmpty*
**if**(partitions!=**null****else**{
partitionSpecList=**new****return****public**String formatString(Recordr,List**throws**UnsupportedEncodingException{
StringBuffer line=**new**StringBuffer();
**int****for**(**int**i =0; i < cols; ++i) {
*//BIGINT, DOUBLE, BOOLEAN, DATETIME,STRING, DECIMAL, MAP, ARRAY;***switch**(type){
******case*BIGINT***:
line.append(r.getBigint(i));
**break**;
**case*DOUBLE***:
line.append(r.getDouble(i));
**break**;
**case*BOOLEAN***:
line.append(r.getBoolean(i));
**break**;
**case*DATETIME***:
line.append(r.getDatetime(i));
**break**;
**case*STRING***:
line.append(r.getString(i));
**break**;
**case*DECIMAL***:
line.append(r.getDecimal(i));
**break**;

**default**:
**throw new**RuntimeException(**"Unknown column type: "****if**(i<cols-< span="">1){
line.append(**","****return**