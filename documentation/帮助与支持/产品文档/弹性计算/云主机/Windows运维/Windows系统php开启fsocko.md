**Windows系统php开启fsockopen函数**

在安装Discuz 和 phpwind程序时需要开启fsockopen函数，开启方法如下：

php环境配置好之后会有个php.ini文件，这是php的配置文件，以Windows 2008一键安装环境为例，

1.php.ini文件在服务器的C:\websoft\php-5.5.7目录下，其他方法安装的php环境可以在磁盘中搜索一下。

![1.png](https://img1.jcloudcs.com/cms/93b71cc4-1c9b-4b0a-b8c9-018c388bacaf20180104094631.png)

2.找到php.ini文件，用记事本打开，查找 allow_url_fopen = 看看后面是 off 还On ，如果是off 那就修改成On。

![2.png](https://img1.jcloudcs.com/cms/251ea89b-f6f0-4f7c-9183-b705380dac9620180104094809.png)

3.在php.ini文件中继续查找extension=php_openssl.dll，extension=php_openssl.dll这段代码前面有个 ; 号，将 ; 号删除，然后保存。

![3.png](https://img1.jcloudcs.com/cms/96c0d3a6-1268-4632-ada1-599723d5710d20180104094913.png)

4.最后重启IIS，打开IIS信息服务管理器，选择右侧的“重新启动”，重启后fsockopen函数即为正常开启。

![4.png](https://img1.jcloudcs.com/cms/0008bd83-d87b-4356-be90-350200e48f8720180104095006.png)

如无法解决您的问题，请向我们提工单。