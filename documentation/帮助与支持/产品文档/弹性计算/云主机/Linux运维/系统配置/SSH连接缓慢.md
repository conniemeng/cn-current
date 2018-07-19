# **SSH连接缓慢**

[转至元数据结尾](http://cf.jd.com/pages/viewpage.action?pageId=88357149#page-metadata-end)[转至元数据起始](http://cf.jd.com/pages/viewpage.action?pageId=88357149#page-metadata-start)

#

# **内容概述：**

用户在使用ssh连接linux云主机的时候会发生连接缓慢的情况，这是由于server端的sshd会去DNS查找访问clientIP的hostname，如果DNS无法连接就会耗费大量时间等待DNS超时。

本文以centos 6.8 64位为例，指导如何配置ssh文件，解决ssh连接缓慢问题。

# **正文：**

第一步：编辑/etc/ssh/sshd_config，将“Use DNS”的参数修改为“no"，执行：

vi /etc/ssh/sshd_config

将UseDNS 更改为no

/#ShowPatchLevel noUseDNS no

第二步：重启sshd进程使配置生效，执行：

/etc/init.d/sshd restart