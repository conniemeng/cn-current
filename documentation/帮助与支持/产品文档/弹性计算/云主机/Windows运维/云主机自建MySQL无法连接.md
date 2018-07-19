**云主机自建MySQL无法连接**

云主机自建MySQL无法连接，提示is not allowed to connect to this MySQL serverConnection closed by foreign host.

![QQ截图20171211232735.jpg](https://img1.jcloudcs.com/cms/02649b29-c384-4999-b1cc-9d853abad66220171211233832.jpg)

请确认MySQL是否打开远程登录。

打开远程登陆有两种方法。

（1 ）改表：在本机登入MySQL 后，更改 “mysql” 数据库里的 “user” 表里的 “host” 项，从 ”localhost” 改为 '%'。

登入mysql后，更改 "mysql" 数据库里的 "user" 表里的 "host" 项，从"localhost"改称"%"
mysql -u root -p
mysql>use mysql;
mysql>update user set host = '%' where user = 'root';
mysql>select host, user from user;

（2 ）授权法：为MySQL创建一个 远程连接的用户

mysql>GRANT ALL PRIVILEGES ON /*./* TO 'root'@'%'WITH GRANT OPTION;

//赋予任何主机访问数据的权限

mysql>FLUSH PRIVILEGES;

//修改生效