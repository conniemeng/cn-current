1.配置Nginx：

打开配置文件

/#vi /etc/nginx/nginx.conf

按i进入编辑模式，在server区段中修改location代码：

location / {

index index.html index.php;

}

在server区段中添加代码：

location ~ \.php$ {

root html;

fastcgi_pass 127.0.0.1:9000;

fastcgi_index index.php;

fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

include fastcgi_params;

}

按esc键退出编辑模式，输入：wq保存并退出。

然后重启web service和php-fpm：

/#systemctl restart nginx.service

/#systemctl restart php-fpm.service

2.获取WordPress安装源码：

/#wget --no-check-certificate 'https://wordpress.org/latest.tar.gz'

3.将源码解压缩到nginx访问路径中：

/#tar -xzf latest.tar.gz -C /usr/share/nginx/html

4.更改与备份html文件夹现有文件：

/# cd /usr/share/nginx/html

/# mv index.html index.html.bak

5.移动文件

/# mv /usr/share/nginx/html/wordpress//* /usr/share/nginx/html

6.访问服务器的公网IP地址，看到如下wordpress安装界面，按照提示，进行分步安装

![](https://img1.jcloudcs.com/cms/df5fd26b-4c37-4115-8d45-a398bc874f7720170313153403.png)

7.输入已经创建的云数据库的信息，注意DataHost中填写刚创建的云数据库的Master域名。点击提交。

![](https://img1.jcloudcs.com/cms/653e9170-5321-4836-ae14-c97f5bfb6c7120170313153422.png)

8.这一步出错的原因是，网站本身对html文件夹没有读写权限。此处我们可以按照提示，手动创建文件：/#vim /usr/share/nginx/html/wp-config.php，复制WordPress已经提供的内容进入此文件，保存后点击“run the install”即可。

![](https://img1.jcloudcs.com/cms/695e2b31-1a8e-4aec-b8d5-b8ee0d70c3b820170313153438.png)

9.至此，已经连接数据库成功，接下来提供网站管理信息。

![](https://img1.jcloudcs.com/cms/149d5439-39b7-4fbe-a646-05d149af75c220170313153451.png)

10.安装成功

![](https://img1.jcloudcs.com/cms/77ade3b1-9e7f-4ff1-8a76-1238d6afe06420170313153505.png)

登录后，控制台界面如下：![](https://img1.jcloudcs.com/cms/510f472a-38b9-4e27-baab-7cbeea1a480520170313153516.png)

博客首页：

![](https://img1.jcloudcs.com/cms/cb79395e-259f-411c-9b02-74310cadabdc20170313153529.png)