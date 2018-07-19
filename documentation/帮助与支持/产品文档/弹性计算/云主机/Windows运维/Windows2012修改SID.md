**Windows2012修改SID**

SID也就是安全标识符（Security Identifiers），是标识用户、组和计算机帐户的唯一的号码。在云上安装AD和我们线下安装AD步骤其实一样，但客户端加入域的步骤稍有不同，需要先修改客户端的SID，这是因为云服务器系统采用的同一个镜像，所以SID是相同的，如果不修改，在加入域的时候会提示SID相同，因此我们需要修改服务器的SID，修改前建议您参考：《[制作私有镜像](https://www.jcloud.com/help/detail/312/isCatalog/1 "https://www.jcloud.com/help/detail/312/isCatalog/1")》创建一个私有镜像，一旦修改失败造成系统异常，可以通过镜像恢复系统。修改操作会重启服务器系统，并且重新进入设置页面，建议您通过控制台终端登陆操作；

首先，cd C:\Windows\System32\Sysprep进入Sysprep目录，然后执行sysprep就可以打开系统准备工具，勾选“通用”后点击确定：

![JCloud20171219180445.jpg](https://img1.jcloudcs.com/cms/73bbb556-9303-4d75-8b49-467b5a18a9a420171219181337.jpg)

提示Sysprep正在工作：

![JCloud20171219180515.jpg](https://img1.jcloudcs.com/cms/87d8f5b2-8314-487c-bea1-457ef7963b0b20171219181349.jpg)

重新进入设置页面：

![JCloud20171219180756.jpg](https://img1.jcloudcs.com/cms/399f0bb1-9cee-4ce2-bd7c-2038ecaabca720171219181402.jpg)

点击下一步>接受，之后重新输入密码：

![JCloud20171219180843.jpg](https://img1.jcloudcs.com/cms/78482f86-c089-4845-a8e4-1e0ff3f32dfd20171219181415.jpg)

按照提示操作，重新登陆到系统中。
输入whoami /user查看SID已经做了修改：

![JCloud20171219181128.jpg](https://img1.jcloudcs.com/cms/4d557c82-cf86-4c66-b3c4-4ea6fca4d18020171219181435.jpg)