请先下载最新版的Ghost，网址： [https://ghost.org/zip/ghost-latest.zip](https://ghost.org/zip/ghost-latest.zip)

### []()[]()操作步骤

1、更新系统

确保你的服务器系统处于最新状态：

[root@softwaretest ~]/# yum -y update

2、安装Node.js

* 安装EPEL：

[root@softwaretest ~]/# yum install epel-release –y

* 安装Node.js 和 npm：

[root@softwaretest ~]/# yum install nodejs npm –enablerepo=epel –y

* 安装进程管理器以便控制Node.js应用程序，这个进程管理器可以保持应用程序一直在运行，运行以下命令进行安装：

[root@softwaretest ~]/# npm install pm2 –g

* 安装后可以通过 node -v 和 npm -v 命令来检查 Node.js 的版本

3、安装Ghost

* 创建Ghost安装目录：

[root@softwaretest ~]/# mkdir -p /var/www/ghost

[root@softwaretest ~]/# cd /var/www/ghost/

[root@softwaretest ghost]/# curl -L [https://ghost.org/zip/ghost-latest.zip -o ghost.zip](https://ghost.org/zip/ghost-latest.zip%20-o%20ghost.zip)

* 解压Ghost安装包：

[root@softwaretest ghost]/# yum install zip unzip –y

[root@softwaretest ghost]/# unzip ghost.zip

* 使用npm安装Ghost，如果报错，请再次执行安装命令。

[root@softwaretest ghost]/# npm install -production

* 安装完成后用 npm start 命令启动ghost，检查有没有安装成功
* 从示例配置文件复制并新建 Ghost 配置文件 config.js：

[root@softwaretest ghost]/# cp config.example.js config.js

* 配置config.js文件中的URL为自己的域名:

[root@softwaretest ghost]/# vi config.js

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-20.png)

* 使用进程管理器来配置Ghost永久运行：

[root@softwaretest ghost]/# NODE_ENV=production pm2 start index.js –name “ghost”

* 开启/停止/重启ghost：

[root@softwaretest ghost]/# pm2 start ghost

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-21.png)

[root@softwaretest ghost]/# pm2 stop ghost

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-22.png)

[root@softwaretest ghost]/# pm2 restart ghost

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-23.png)

Ghost安装成功