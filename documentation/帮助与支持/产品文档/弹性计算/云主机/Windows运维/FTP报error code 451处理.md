## FTP报Error code 451处理方法

### 现象描述

使用Windows Server IIS搭建的FTP服务器在上传文件夹或者文件的时候，如果文件夹或者文件名称中英文混和，则会出现以下错误提示框：

![](http://cms.jcloud.com/ueditor/themes/default/images/spacer.gif) ![TimLine图片20180312125107.png](http://img1.jcloudcs.com/cms/b97bd575-4ead-4322-9e43-2e117a32236b20180312125116.png)

### 处理步骤

1. 
点击任务栏左下角红框处启动“服务器管理器”，点击右上角红框处工具按钮，选择IIS管理器。

![IIS1.JPG](http://img1.jcloudcs.com/cms/6e93fe73-0766-4904-aecd-49395adf774720180312130457.JPG)

2. 在IIS管理器左侧网站页面逐级选择FTP站点，点击右侧红框处**高级设置**。

![IIS2.JPG](http://img1.jcloudcs.com/cms/ccfa8135-edac-42cc-abed-16d9fc9e638620180312130517.JPG)

3. 将“允许UTF8”从 “True” 改为 “False”，点击确定。

![IIS3.JPG](http://img1.jcloudcs.com/cms/7e7cd5b5-5ae3-4e68-a118-f2e32468939c20180312130534.JPG)

4. 点击右侧红框处**重新启动**按钮即可重启服务器， 问题可以得到解决。

![IIS4.JPG](http://img1.jcloudcs.com/cms/6969247f-e981-476e-a917-45f27c8cfa8220180312130543.JPG)