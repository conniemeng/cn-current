# **API概览**

### **关于Service的操作**

API

描述GetService

得到该账户下所有Bucket

### **关于Bucket的操作**

API

描述Put Bucket

创建BucketPut Bucket Referer

设置Bucket的防盗链规则Get Bucket Referer

查看Bucket的防盗链规则Delete Bucket

删除BucketGet Bucket(List Object)

获得Bucket中所有Object的信息

### **关于Object的操作**

API

描述PutObject

上传objectGetObject

获取ObjectDeleteObject

删除Object

### **关于Multipart Upload的操作**

API

描述Initiate Multipart Uploade

初始化MultipartUpload事件Upload Part

分块上传文件Complete Multipart Upload

完成整个文件的Multipart Upload上传Abort Multipart Upload

取消Multipart Upload事件List Multipart Uploads

罗列出所有执行中的Multipart Upload事件List Parts

罗列出指定Upload ID所属的所有已经上传成功Part