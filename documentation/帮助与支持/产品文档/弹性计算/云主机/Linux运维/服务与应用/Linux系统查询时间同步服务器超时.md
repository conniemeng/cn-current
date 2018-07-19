**Linux系统查询时间同步服务器超时**

**问题现象**

执行查看时间同步服务器命令报错，如图：

ntpq -p localhost: timed out, nothing received /*/*/*Request timed out

**问题原因**

ntp配置文件写的是调用ipv6地址执行会超时。

**解决办法**

**方法一.使用ipv4地址方式查询，执行：**

ntpq -4p

可以正确查询时间同步服务器，如图：

![2.png](https://img1.jcloudcs.com/cms/a0901c8c-f669-4457-92f3-7c5db6eb5a6220171124150143.png)

****

**方法二.关闭ipv6地址，执行：**
sh -c 'echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6' ntpq -p

查询结果如图：

![3.png](https://img1.jcloudcs.com/cms/54547a88-ce1f-4c70-ac38-e0cc2e3ee03d20171124150545.png)

如无法解决您的问题，请向我们提工单。