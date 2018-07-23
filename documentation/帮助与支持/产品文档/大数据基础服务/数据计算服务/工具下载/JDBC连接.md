**如何通过JDBC进行数据计算服务连接**

数据计算服务JDBC驱动基于presto-jdbc开发.

JDBC连接信息配置例如：

String url = "jdbc:xdata://gateway.jcloud.com/instance_name";

String accessId = "xxxxxx";

String accessKey = "xxxxxxx";

其中url中的instance_name为instance名称，instance也可以通过property进行设置，如：

properties.setProperty("instance", "instance_name");

目前支持华南，华北，需要在properties中增加对region的设置，华南为HN_GZ ，华北为HB_BJ

properties.setProperty("region", "HB_BJ");

点击下载新版JDBC客户端![](http://cms.jcloud.com/ueditor/dialogs/attachment/fileTypeImages/icon_rar.gif)[xdata-jdbc-0.1-SNAPSHOT.zip](https://img1.jcloudcs.com/cms/b264ff36-2657-4fda-8a9c-72549163401d20180510164147.zip "xdata-jdbc-0.1-SNAPSHOT.zip")