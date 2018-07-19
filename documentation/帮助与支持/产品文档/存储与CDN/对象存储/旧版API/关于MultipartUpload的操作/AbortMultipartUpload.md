### **AbortMultipartUpload**

该接口可以根据用户提供的Upload ID终止其对应的Multipart Upload事件。当一个Multipart Upload事件被中止后，其UploadId也一同作废，且该Multipart Upload中的所有已上传的Part所占用的存储空间都会被释放。

### **请求语法**

DELETE /BucketName/ObjectName?uploadId=UploadIdHTTP/1.1
Host: BucketName. s-bj.jcloud.com
Date: GMT Date
Authorization: signatureValue

细节分析： 如果输入的Upload Id不存在，OSS会返回404错误，错误码为： NoSuchUpload。

### **请求示例**

DELETE /oss-test-mul?uploadId=8BE181320822A189 HTTP/1.1
Date: Wed, 12 Jul 2017 13:36:37 GMT
Authorization: jingdong 298718BEDE59FF1B2E96A3152937D37B:FGic1+W0ggmbzXiwwwfbnJrQEkE=
Host: oss-test.s-bj.jcloud.com
Connection: Keep-Alive

**返回示例**

HTTP/1.1 204 No Content
Server: nginx
Date: Wed, 12 Jul 2017 13:36:36 GMT
Connection: keep-alive
x-jss-request-id: A27711FCD88D6666