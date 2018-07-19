## **自建mysql数据库修改最大连接数**

连接在云主机上搭建的mysql数据库时，有时会报1040错误，提示过多连接，如图

![mysql3.JPG](https://img1.jcloudcs.com/cms/448421ac-7d7e-43ed-b891-2137505488dc20180109113610.JPG)

此时需要修改/etc/my.cnf文件，在[mysqld]部分中新增或修改max_connections=N条目，默认值为100，可根据需要进行调整，如图

![mysql2.JPG](https://img1.jcloudcs.com/cms/08dd9a7e-82f4-40c9-8767-57fb704d5b9a20180109114120.JPG)

修改完后wq保存文件，重启mysql数据库，验证是否生效。