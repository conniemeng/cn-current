**SDK-Python**

1.安装boto3

使用aws sdk-python前，您需要先安装boto3包，命令如下（请确定pip已经安装）：

pip install boto3

2.创建client

下面我们给出了一个创建client的例子，更多信息请参考：[http://boto3.readthedocs.io/en/latest/reference/services/s3.html](http://boto3.readthedocs.io/en/latest/reference/services/s3.html)

import boto3
ACCESS_KEY =‘your accesskey’
SECRET_KEY = ‘your secretkey’
s3 = boto3.client(
's3',
aws_access_key_id=ACCESS_KEY,
aws_secret_access_key=SECRET_KEY,
/#下面给出一个endpoint_url的例子
endpoint_url='http://s3.cn-north-1.jcloudcs.com'
)
/#use s3 client to create bucket、put object....