**linux删除文件提示"Operation not permitted"**

**问题现象:**

用户在云主机内对文件做删除,移动等操作，会提示"Operation not permitted"错误，无法操作成功，如下图；

**![image.png](https://img1.jcloudcs.com/cms/b7bd352c-7322-4058-8958-8b16643851b520180327164158.png)**

****

**问题原因:**

相关文件被添加了 i 保护属性导致操作失败。

**处理方法：**

使用lsattr命令查看文件属性，可以看到文件被添加了 i 的属性；此属性表示文件不可被修改，也无法删除；****

**![image.png](https://img1.jcloudcs.com/cms/b13454ec-2def-4f80-834a-363807c7aed920180327164431.png)**

使用chattr命令将i属性删除；

**![image.png](https://img1.jcloudcs.com/cms/34fc5266-6198-480b-b1c5-12f49807c00e20180327164639.png)**

将i属性删除后，在操作此文件便会正常；