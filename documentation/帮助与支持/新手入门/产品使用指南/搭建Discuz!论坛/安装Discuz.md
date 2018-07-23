1、下载Discuz安装包

/# wget ‘[http://download.comsenz.com/DiscuzX/3.1/Discuz_X3.1_TC_UTF8.zip](http://download.comsenz.com/DiscuzX/3.1/Discuz_X3.1_TC_UTF8.zip)’

2、查询目前目录底下是否有Discuz压缩文件

/# ls

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-97.png)

3、安装unzip（为了对zip压缩文件进行解压）

/# yum install unzip –y

4、解压缩Discuz_X3.1_TC_UTF8.zip

/# unzip Discuz_X3.1_TC_UTF8.zip

5、再次查询目前目录底下会多三个文件夹（readme、upload、utility）

（可以在自己本机也下载一个Discuz_X3.1_TC_UTF8.zip进行比对）

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-98.png)

6、将upload文件夹内的所有文件及文件夹移动到服务器的/var/www/html/目录中

/# mv upload//* /var/www/html

7、在客户端访问公网IP进入，就能看见Discuz安装界面，点击“我同意”

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c.png)

8、接着如果看到目录文件权限不足，就需要回到putty将文件夹的权限打开才能继续安装，如果没有出现错误则请继续往下

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-1.png)

**打开目录文件夹的权限：**

先将目录切换到服务器的/var/www/html/目录下

/# cd /var/www/html/

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-99.png)

修改以下几个目录的权限（config、data、uc_server/data/、uc_client/data/cache）

/# chmod -R 777 config/ data/ uc_server/data/ uc_client/data/cache/

重新刷新浏览器chrome，所以状态都能呈现打勾，就能拉倒底部点击下一步

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-2.png)

9、选择权限安装Discuz! X（含 UCenter Server）点击下一步

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-3.png)

10、填写数据库信息的部分需要修改数据库密码（输入MySQL的root密碼），填写管理员信息的部分需要输入管理员密码（这是Discuz论坛的管理员密码请记好）、重复密码（管理员密码），完成后点击下一步

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-4.png)

11、等待安装

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-5.png)

12、安装完成后点右下角有一行小字（您的论坛已完成安装，点此访问）

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/https-sky172839465-gitbooks-io-discuz-on-linux-c-6.png)

13、回到浏览器chrome出现以下界面，说明您的论坛可以正常工作访问了。

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-100.png)