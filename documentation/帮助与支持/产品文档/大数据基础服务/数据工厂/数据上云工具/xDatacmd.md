# xDatacmd使用说明

xDatacmd工具以客户端命令行的形式实现数据的批量上传下载处理，支持命令行交互模式和批处理模式；对于批处理模式提供多种可选择的格式样式输出。目前支持本地文件上载、数据库（mysql、oracle、sql server、DB2等）的上载、数据仓库表下载。

## 如何下载xDatacmd

下载地址如下：[https://xdata.jcloud.com/map/spsdownload/downLoadClient.action](https://xdata.jcloud.com/map/spsdownload/downLoadClient.action)

## 运行环境要求

lJDK1.7及以上

## 如何配置

使用命令行时，需要配置xdata_config.ini。下载xDatacmd客户端文件后，进行解压缩。进入conf文件，找到xdata_config.ini文件进行配置，添加用户默认数据库以及用户认证信息。如下图所示：

database_name=<填写默认数据库>

access_id=<填写access id>

access_key=<填写access key>

end_point=http://bds-api.jcloud.com

https_check=true

retry_time=3

engine=auto

下图是配置的测试示例：
database_name=demo

access_id=22D3f122B37E11E59EC733AABDT34A0x

access_key=N87548x

end_point=http://bds-api.jcloud.com

https_check=true

retry_time=3

engine=auto

备注：如何获得access_id，access_key

在控制台页([https://xdata.jcloud.com/console_page?dataCenter=bj_02](https://xdata.jcloud.com/console_page?dataCenter=bj_02))

""

## 如何使用批量上传下载功能

完成xdata_config.ini后，即可通过命令使用上传下载功能。xDatacmd提供了两种模式：交互模式和非交互模式。交互模式可以持续接收用户输入的命令，适用于需要多次连续输入命令的情况。非交互模式可以完成一次命令的上传和下载。

接下来将详细介绍这两种模式。

### 如何使用交互模式

进入下载的xDatacmd的bin文件中，这个文件夹下有两个脚本，如果是linux系统使用xDatacmd，如果是windows系统使用xdatacmd.bat。

### n进入交互式模式命令

### 1.语法

./xdatacmd

### 2.说明

进入交互式模式。参数说明：无

### n帮助命令

### 1.语法

HELP

### 2.说明

命令帮助。参数说明：无

### 3.示例

命令帮助：

help;

### n退出命令

### 1.语法

QUIT

### 2.说明

退出交互模式。参数说明：无

### 3.示例

退出交互模式：

quit;

### n本地文件上传

### 1.语法

tableupload[options]

### 2.说明

使用tableupload命令指定本地文件和目标加载的数据库及表名进行上传加载。

### 3.参数说明：

**参数名称**

**描述**-bs

-block-size-c

-charset-cp

-compress-dbr

-discard-bad-records

action(true|false), default false-dfp

-date-format-pattern-fd

-field-delimiter-h

-header-mbr,

-max-bad-records-ni

-null-indicator-rd

-record-delimiter-s

-scan-sd

-session-dir-threads

number of threads, default 1

### 4.示例

上传：

tableupload log.txttest_db.test_table/p1="b1"/p2="b2";

### noracle/mysql/DB2等数据库数据上传

### 1.语法

dbupload–sql”上传数据的查询语句”<[database.]table[/partition]>

### 2.说明

使用dbupload命令指定将对应sql查询的指定的数据库的结果集，上传至目标数据库中。

### 3.参数说明：

### 4.示例

上传：

/#example of xdatacmd/conf/xdata_config.ini

access_id = <填写access_id>

access_key = <填写access_key>

end_point = http://bds-api.jcloud.com

database_name =

dbupload_ip =

dbupload_database_name =

dbupload_user_name = < msql\orcale\db2登录账号>

dbupload_password = < msql\orcale\db2登录密码>

dbupload_port =<msql\orcale\db2< span="">端口号>

dbupload_database_type = <从哪种数据库中上传数据mysql\orcale\db2>

dbupload_sql = <上传数据的查询语句>

dbupload_if_delete = <true >

### n下载

### 1.语法

tabledownload [options]

### 2.说明

使用tabledownload命令下载xData数据。

### 3.参数说明：

**参数名称**

**描述**-c

-charset-cp

-compress-dfp

-date-format-pattern-fd

-field-delimiter-h

-header-ni

-null-indicator-rd

-record-delimiter-sd

-session-dir-threads

number of threads, default 1

### 4.示例

下载：

tabledownload db.test_table/p1="b1",p2="b2"log.txt

### n断点续传

### 1.语法

tableresume [session_id] [-force]

### 2.说明

使用tableresume命令，通过输入对应的session_id来进行断点续传。

### 3.参数说明：

-f,-forceforce resume

### 4.示例

断点续传：

tableresume 20160926135833b1a6429378e51462;

### n数据库断点续传

### 1.语法

dbresume [session_id] [-force]

### 2.说明

使用dbresume命令，通过输入对应的session_id来进行断点续传。

### 3.参数说明：

-f,-forceforce resume

### 4.示例

断点续传：

dbresume 20161017151454930f3e679ad5b50b;

### n查看历史

### 1.语法

tableshow history [options]

### 2.说明

使用tableshow命令，查看本地生成的数据上传下载历史记录。

参数说明：

-n,-number

### 3.示例

查看历史：

Tableshow history -n 10;

### n清除历史

### 1.语法

Tablepurge [n];

### 2.说明

使用tablepurge命令，根据输入的天数，可以清除本地生成的相应的数据上传下载历史记录，默认清除3天前的历史记录。

参数说明：无

### 3.示例

清除历史：

Tablepurge 10;

### 如何使用非交互模式

### n进入非交互模式：

### 1.语法

dcscmd [OPTION]

### 2.参数说明

**参数名称**

**描述**--help

(-h)for help-e

execute command

### 3.详细命令示例

显示非交互模式xdatacmd命令使用说明

数据上传

./xdatacmd -e "tableupload /home/dbustest.csv datatest1.datatest"

数据下载

./xdatacmd -e "tabledownload datatest1.datatest/home/dbustest.csv "

断点续传

./xdatacmd -e "tableresume20160926135833b1a6429378e51462"

查看历史

./xdatacmd -e "Tableshowhistory -n 10"

清除历史

./xdatacmd -e "Tablepurge10"