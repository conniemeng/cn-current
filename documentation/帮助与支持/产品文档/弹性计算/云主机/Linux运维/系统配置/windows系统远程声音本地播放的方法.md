问题现象:
windows系统远程连接后，右下角的声音显示红叉，无法播放远程声音；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/112115ymlawlnews6mpmgg.png)
处理方法:
可以通过设置本地电脑远程桌面工具的方法，将远程的声音在本地电脑上播放；
云主机内请先调整下如下设置；
windows 2008系统：
1 远程连接后，点击开始-管理工具-远程桌面服务-远程桌面会话主机；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/113138ufk3np35z5i3g9in.png)
2 双击rdp-tcp，选择客户端设置，将音频和视频播放的勾选取消；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/113358upkidz7eikrhly70.png)
3 点击开始-运行-输入services.msc，找到“Windows Audio”服务，将此服务设置为自动，并启动下，之后将此次的远程连接关闭；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/113727oahw3npbufu7zy3n.png)
windwos 2012系统：
1 打开windwos powershell，输入gpedit.msc，打开组策略；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/114139lqyzw5ywch2w5chg.png)
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/114144allmcexrd2gwsdde.png)
2 依次点击“计算机配置”-“管理模版”-“windows 组件”-“远程桌面服务”-“远程桌面会话主机”-“设备和资源重定向”，打开“允许音频和视频播放重定向”，选择“已启用”;
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/114522zz6qep1066c1pr0g.png)
3 继续在windwos powershell中输入services.msc打开服务，找到“Windows Audio”服务，将此服务设置为自动，并启动下，之后将此次的远程连接关闭；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/114654gg7q08o7nx77z76z.png)
以上配置调整完成后，打开本地远程桌面软件，点击“选项”-“本地资源”，在远程声音处点击“设置”，弹出的选项卡中的远程音频播放处，选择“在此计算机中播放”，点击确定；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/112607clztc36c3wnn3x3n.png)
再次连接后，可以看到右下角声音处显示已经正常，此时在远程打开音频文件，本地是可以正常听到声音的；
![](http://wiki.keepcloud.cn/data/attachment/forum/201804/13/114829f299ip6zj6p29e2e.png)