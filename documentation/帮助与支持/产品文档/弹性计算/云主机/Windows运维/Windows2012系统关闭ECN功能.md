**Windows2012系统关闭ECN功能**

远程桌面登陆服务器后点击Windows Power Shell，输入netsh int tcp show global，查看ECN功能状态：

![QQ截图20171120111418.png](https://img1.jcloudcs.com/cms/33fea0e9-7dbe-49d4-a82f-ff69a028d7b420171120111645.png)

输入netsh int tcp set global ecn=disable后回车，正常返回确定消息，再次输入netsh int tcp show global查看，ECN功能被正常关闭。

![QQ截图20171120111442.png](https://img1.jcloudcs.com/cms/e05ca975-4687-480a-82c8-b273d6062b0d20171120111756.png)

如无法解决您的问题，请向我们提工单。