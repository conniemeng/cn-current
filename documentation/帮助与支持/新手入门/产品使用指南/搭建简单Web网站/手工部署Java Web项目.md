# **手工部署Java Web项目**

**搭建JAVA Web开发环境**

## **测试环境**

Ubuntu 16.04.2 LTS

Kernel：4.4.0-62-generic

## **操作流程**

1. 
创建目录
1. 
下载安装JDK
1. 
配置环境变量
1. 
下载安装Tomcat
1. 
使用浏览器连接服务器
1. 
运行一个示例程序

## **具体步骤**

### **创建目录**

/# mkdir /usr/local/java/jdk /usr/local/java/tomcat

### **下载安装JDK**

浏览器输入下载网址：

[http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html?spm=5176.doc51376.2.7.3xQYcw](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html?spm=5176.doc51376.2.7.3xQYcw)

点击单选按钮，只有选择Accept License Agreement选项后才可以下载，所以无法直接使用wget来获取jdk的软件包

![E:\云途项目\陆\源文件\图片\28.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-28-png.png)

选择Accept License Agreement后，内容变化，现在可以下载了，但是现在还无法直接使用wget下载到云主机，需要一些辅助步骤拿到jdk的真实链接

![E:\云途项目\陆\源文件\图片\29.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-29-png.png)

按下F12（谷歌浏览器），弹出调试工具窗口，选择Network，点击需要安装的jdk链接

![E:\云途项目\陆\源文件\图片\30.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-30-png.png)

复制jdk软件包的真实链接

![E:\云途项目\陆\源文件\图片\30 - 副本.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-30-png-1.png)

### 进入/usr/local/java/jdk目录，下载jdk软件包

/# cd /usr/local/java/jdk

/# wget http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.tar.gz?AuthParam=1503024084_c6d31266da454295dea1737f66cab043

![E:\云途项目\陆\源文件\图片\31.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-31-png.png)

下载结束后，使用ls查看，发现多了一个文件

/# ls

![E:\云途项目\陆\源文件\图片\2017-08-18_130958.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_130958-png.png)

### **修改软件包名**

/# mv jdk-8u144-linux-x64.tar.gz\?AuthParam\=1503024084_c6d31266da454295dea1737f66cab043 jdk-8u144-linux-x64.tar.gz

![E:\云途项目\陆\源文件\图片\2017-08-18_131132.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_131132-png.png)

### **解压缩**

/# tar -zxvf jdk-8u144-linux-x64.tar.gz

![E:\云途项目\陆\源文件\图片\2017-08-18_131337.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_131337-png.png)

### **配置环境变量**

/# vim /etc/profile

在/etc/profile文件最后添加如下内容

/#set java environment

export JAVA_HOME=/usr/local/java/jdk/jdk1.8.0_144

export JRE_HOME=/usr/local/java/jdk/jdk1.8.0_144/jre

export CLASSPATH=.:$JAVA_HOME/lib$:JRE_HOME/lib:$CLASSPATH

export PATH=$JAVA_HOME/bin:$JRE_HOME/bin/$JAVA_HOME:$PATH

![E:\云途项目\陆\源文件\图片\33.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-33-png.png)

保存并退出文件。

查看是否配置成功

/# java –version

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-105.png)

到此，JDK已成功安装，环境变量成功配置

### **下载安装Tomcat**

### **下载Tomcat软件包**

/# cd /usr/local/java/tomcat

/# wget [http://apache.website-solution.net/tomcat/tomcat-8/v8.5.20/bin/apache-tomcat-8.5.20.tar.gz](http://apache.website-solution.net/tomcat/tomcat-8/v8.5.20/bin/apache-tomcat-8.5.20.tar.gz)

![E:\云途项目\陆\源文件\图片\34.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-34-png.png)

### **解压缩**

/# tar -zxvf apache-tomcat-8.5.20.tar.gz

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-106.png)

### **编辑setclasspath.sh脚本**

vim /usr/local/java/tomcat/apache-tomcat-8.5.20/bin/setclasspath.sh

![E:\云途项目\陆\源文件\图片\35.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-35-png.png)

### **启动Tomcat**

/# cd /usr/local/java/tomcat/apache-tomcat-8.5.20/bin

/# ./startup.sh

![E:\云途项目\陆\源文件\图片\36.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-36-png.png)

### **使用浏览器输入连接服务器**

默认的端口号是8080，在浏览器地址栏填写云主机ip地址和端口号，格式为：IP:PORT

![E:\云途项目\陆\源文件\图片\2017-08-18_122228.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_122228-png.png)

看到图示界面，表示Tomcat启动成功。

查看/usr/local/java/tomcat/apache-tomcat-8.5.20目录下有webapps目录，该目录是项目目录，可将自己的项目放入其中。该目录下有示例项目，可在浏览器中查看运行

![E:\云途项目\陆\源文件\图片\2017-08-18_122931.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_122931-png.png)

### 运行一个示例程序

### 点击Examples

![E:\云途项目\陆\源文件\图片\2017-08-18_123600.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_123600-png.png)

JSP Examples

![E:\云途项目\陆\源文件\图片\2017-08-18_123659.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_123659-png.png)

点击Execute

![E:\云途项目\陆\源文件\图片\2017-08-18_123738.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_123738-png.png)

运行结果如图

![E:\云途项目\陆\源文件\图片\2017-08-18_123816.png](http://cloudway.jcloud.com/wp-content/uploads/2017/05/e-2017-08-18_123816-png.png)