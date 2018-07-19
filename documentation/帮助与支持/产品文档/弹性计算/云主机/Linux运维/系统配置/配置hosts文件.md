# **配置hosts文件**

[转至元数据结尾](http://cf.jd.com/pages/viewpage.action?pageId=88347019#page-metadata-end)[转至元数据起始](http://cf.jd.com/pages/viewpage.action?pageId=88347019#page-metadata-start)

#

# **内容概述：**

以centos 6.8 64位为例，指导如何在系统内部配置host文件，实现本地对hostname的DNS解析。

# **正文：**

第一步：查看并编辑hosts文件。在hosts文件中将本机hostname“hostdemo”与127.0.0.1绑定。执行：

cat /etc/hostsvi /etc/hosts

第二步：ping主机hostname，可以看到结果，本地的DNS已经将“hostdemo”解析成了127.0.0.1。执行：

ping hostdemo

[](https://img1.jcloudcs.com/help/pzhostswj1090.html)