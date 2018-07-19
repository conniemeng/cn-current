**Mysql重置root密码方法**

****

****

**Linux系统：**

如果使用 MySQL 数据库忘记了账号密码，可以通过调节配置文件，跳过密码的方式登数据库，

在数据库里面修改账号密码，一般默认的账号问 root

1、编辑 MySQL 配置文件 my.cnf

vi /etc/my.cnf 注意： 以实际 my.cnf 配置文件路径为准

[mysqld]skip-grant-tables /#增加

2、重启 MySQL 服务

注意：以实际 MySQL 启动脚本路径为准

/etc/init.d/mysqld restart

3、登录数据库

/usr/bin/mysql 输入如下命令：

注意：以实际 MySQL 执行文件路径为准

mysql> USE mysql;
mysql> UPDATE user SET Password = password (‘新密码’) WHERE User = ‘root’ ;
mysql> flush privileges ;
mysql> quit

4、删除或者注释第一步骤中添加的 spip-grant-tables

![1.png](https://img1.jcloudcs.com/cms/4ef371e1-55cf-40c3-9a15-54cba0af93bd20171211101624.png)

5、重启 MySQL 服务

/etc/init.d/mysqld restart

6、使用新密码测试

**Windows系统：**

操作系统：Windows Server 2008 R2 标准版 SP1 64位中文版；MySQL 版本：mysql Ver 14.12 Distrib 5.0.87, for Win32 (ia32)

其他的版本方法类似。

1、切换 MySQL 安装的 bin 目录下。

默认安装的目录为：C:\Program Files (x86)\MySQL\MySQL Server 5.0\bin

![2.png](https://img1.jcloudcs.com/cms/c31a3fe3-1df2-47dc-bf54-83473b9d9a2f20171211102342.png)

注意： MySQL 的实际安装目录和默认安装目录不同，请根据实际安装的路径自行修改。

2、停止mysql服务，执行
net stop mysql

![3.png](https://img1.jcloudcs.com/cms/b04a5344-5720-413a-a5c6-0ec8f9745efb20171211102552.png)

3、以安全模式启动 MySQL
mysqld-nt.exe —skip-grant-tables

![4.png](https://img1.jcloudcs.com/cms/51202849-afbb-4ac4-9fbe-cc7af837dc4420171211102728.png)

注意：这个窗口保持现状，不要关闭

4、登录 MySQL 服务（另外新开一个 cmd 窗口），执行

mysqld-nt.exe —skip-grant-tables

![5.png](https://img1.jcloudcs.com/cms/0cc19313-6b87-4345-a966-c4224de5c3c520171211102958.png)

提示输入密码时直接回车即可。

5、修改密码，执行
>use mysql;
>update user set Password=password(‘123456’) where User=’root’;
>flush privileges;
>exit

![6.png](https://img1.jcloudcs.com/cms/11eb2758-b8ac-4d83-b03f-b2f77ef6809520171211103135.png)

不建议修改密码为：123456，这样的密码太简单，因为做演示，所以设置为简单密码。密码需要满足密码复杂性要求，需要大小写字母，数字组合，最小长度为 8 位，根据这个密码策略，设置密码。修改完成后退出。

6、在任务管理器里关闭所有 MySQL 的进程，这样前面保持住的窗口就自动关闭。

![7.png](https://img1.jcloudcs.com/cms/c95b4874-6e8a-431c-828d-cc4aaa6f0ba520171211103424.png)

7、启动 MySQL 并测试登录

修改后使用新密码登录。

![8.png](https://img1.jcloudcs.com/cms/2bc14ee5-bf54-47cf-9de4-498a92daf69d20171211103531.png)

修改后使用新密码登录。

![9.png](https://img1.jcloudcs.com/cms/d66e095e-bda6-4046-aa12-d0d936d7916e20171211103612.png)

可以看到新的密码 123456 已经可以登录到 MySQL 数据库，至此重置 MySQL 数据库密码重置完成。

如无法解决您的问题，请向我们提工单。