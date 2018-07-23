## 安装Linux面板

Centos安装脚本
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install-jd.sh && sh install.sh

Ubuntu/Deepin安装脚本

wget -O install.sh http://download.bt.cn/install/install-ubuntu-jd.sh && sudo bash install.sh

Debian安装脚本

wget -O install.sh http://download.bt.cn/install/install-ubuntu-jd.sh && bash install.sh

Fedora安装脚本

wget -O install.sh http://download.bt.cn/install/install-jd.sh && bash install.sh

## 管理Linux面板

停止
service bt stop

启动

service bt start

重启

service bt restart

卸载

service bt stop && chkconfig --del bt && rm -f /etc/init.d/bt && rm -rf /www/server/panel

查看当前面板端口

cat /www/server/panel/data/port.pl

修改面板端口，如要改成8881（centos 6 系统）

echo '8881' > /www/server/panel/data/port.pl && service bt restart iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 8881 -j ACCEPT service iptables save service iptables restart

修改面板端口，如要改成8881（centos 7 系统）

echo '8881' > /www/server/panel/data/port.pl && service bt restart firewall-cmd --permanent --zone=public --add-port=8881/tcp firewall-cmd --reload

强制修改MySQL管理(root)密码，如要改成123456

cd /www/server/panel && python tools.pyc root 123456

修改面板密码，如要改成123456

cd /www/server/panel && python tools.pyc panel 123456

站点配置文件位置

/www/server/panel/vhost

删除域名绑定面板

rm -f /www/server/panel/data/domain.conf

清理登陆限制

rm -f /www/server/panel/data//*.login

查看面板授权IP

cat /www/server/panel/data/limitip.conf

关闭访问限制

rm -f /www/server/panel/data/limitip.conf

查看许可域名

cat /www/server/panel/data/domain.conf

关闭面板SSL

rm -f /www/server/panel/data/ssl.pl && /etc/init.d/bt restart

查看面板错误日志

cat /tmp/panelBoot

查看数据库错误日志

cat /www/server/data//*.err

站点配置文件目录(nginx)

/www/server/panel/vhost/nginx

站点配置文件目录(apache)

/www/server/panel/vhost/apache

站点默认目录

/www/wwwroot

数据库备份目录

/www/backup/database

站点备份目录

/www/backup/site

站点日志

/www/wwwlogs

## Nginx服务管理

nginx安装目录
/www/server/nginx

启动

service nginx start

停止

service nginx stop

重启

service nginx restart

启载

service nginx reload

nginx配置文件

/www/server/nginx/conf/nginx.conf

## Apache服务管理

apache安装目录
/www/server/httpd

启动

service httpd start

停止

service httpd stop

重启

service httpd restart

启载

service httpd reload

apache配置文件

/www/server/apache/conf/httpd.conf

## MySQL服务管理

mysql安装目录
/www/server/mysql

phpmyadmin安装目录

/www/server/phpmyadmin

数据存储目录

/www/server/font

启动

service mysqld start

停止

service mysqld stop

重启

service mysqld restart

启载

service mysqld reload

mysql配置文件

/etc/my.cnf

## FTP服务管理

ftp安装目录
/www/server/pure-ftpd

启动

service pure-ftpd start

停止

service pure-ftpd stop

重启

service pure-ftpd restart

ftp配置文件

/www/server/pure-ftpd/etc/pure-ftpd

## PHP服务管理

php安装目录
/www/server/php

启动(请根据安装PHP版本号做更改，例如：service php-fpm-54 start)

servicephp-fpm-{52|53|54|55|56|70|71} start

停止(请根据安装PHP版本号做更改，例如：service php-fpm-54 stop)

service php-fpm-{52|53|54|55|56|70|71} stop

重启(请根据安装PHP版本号做更改，例如：service php-fpm-54 restart)

service php-fpm-{52|53|54|55|56|70|71} restart

启载(请根据安装PHP版本号做更改，例如：service php-fpm-54 reload)

service php-fpm-{52|53|54|55|56|70|71} reload

配置文件(请根据安装PHP版本号做更改，例如：/www/server/php/52/etc/php.ini)

/www/server/php/{52|53|54|55|56|70|71}/etc/php.ini

## Redis服务管理

redis安装目录
/www/server/redis

启动

service redis start

停止

service redis stop

redis配置文件

/www/server/redis/redis.conf

## Memcached服务管理

memcached安装目录
/usr/local/memcached

启动

service memcached start

停止

service memcached stop

重启

service memcached restart

启载

service memcached reload