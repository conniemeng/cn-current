数据总线支持以Agent方式进行数据写入，具体使用方法如下：

**1.****下载地址：**

[https://xdata.jdcloud.com/map/spsdownload/downLoadAgent.action](https://xdata.jdcloud.com/map/spsdownload/downLoadAgent.action)

**2.****配置说明**

将下载的Agent压缩包，解压到/home/flumedir路径下，在conf文件夹下添加properties文件，例如test.properties，具体配置文件详细说明如下：

**3****定义source**
**属性名称**

**默认值**

**描述**Type

source组件名称filegroups

文件组名称，空格分隔文件组列表filegroups.

指定filegroupName对应的文件路径positionFile

~/.flume/taildir_position.json

记录当前文件访问的位置，生成json记录放在该文件中headers..

头信息，用于区分不同文件中传入的数据byteOffsetHeader

false

是否需要添加字节偏移量skipToEnd

false

如果没有记录读取位置时，是否跳过文件结尾fileHeader

false

Event header中是否添加headerKeyfileHeaderKey

file

文件路径信息，在event header中对应的key值

配置示例:

/#/#定义sources名称

streaming.sources=tailDirSrc

/#/#定义Sourceype:

TAILDIR类型: 该类型可以读取文件夹里的日志，使用时指定一个文件夹，可以读取该文件夹中的所有文件

streaming.sources.tailDirSrc.type=TAILDIR

exec类型: Exec Source在启动时运行给定的Unix命令，并期望进程在标准输出上产生连续的数据

streaming.sources.tailDirSrc.type=exec

streaming.sources.tailDirSrc.command = tail -F /var/log/secure

/#/#定义文件读取位置存储位置

streaming.sources.tailDirSrc.positionFile=/home/flumedir/flumeplugin/data/taildir_position.json

/#/#定义上传文件组

streaming.sources.tailDirSrc.filegroups=one two

/#/#分别定义文件信息

streaming.sources.tailDirSrc.filegroups.one=/home/flumedir/flumeplugin/data/test.txt

streaming.sources.tailDirSrc.headers.one.headerKey=one

streaming.sources.tailDirSrc.filegroups.two=/home/flumedir/flumeplugin/data/test2.txt

streaming.sources.tailDirSrc.headers.two.headerKey=two1

/#/#headerkeyheader

streaming.sources.tailDirSrc.fileHeader=true

/#/#header eventkey

streaming.sources.tailDirSrc.fileHeaderKey=file

****

**4.****定义channel**

配置示例如下：

/#/#定义channel名称

streaming.channels=memoryChannel

/#/#定义channel类型, channel的类型可以配置为memory,file,此处用memory

streaming.channels.memoryChannel.type=memory

/#/#定义memory channel容量大小

streaming.channels.memoryChannel.capacity=1000

/#/#定义transactionCapacity大小, source的ChannelProcessor一次可以向channel中写入的最大event数量，该组件负责在一个事务中移动source中的event到channel中

streaming.channels.memoryChannel.transactionCapacity=1000

****

**5.****定义sink**

StreamingSink参数说明：
属性名称

是否必填

描述Type

是

sinktype名称：com.jcloud.flume.plugin.sink.streaming.StreamingSinkuploadType

是

标识为true:上传给有schema的数据流;false：上传给没有schema的数据流appKey

是

您的京东账号app keyappSecret

是

您的京东账号app secretstreamingName

是

上传数据对应的topic namebatchSize

是

批量提交信息数量serverUrl

否

上传数据对应的服务器地址

配置示例如下：

/#/#sink对应名称

streaming.sinks=streamingSink

/#/#定义sink类型

streaming.sinks.streamingSink.type=com.jcloud.flume.plugin.sink.streaming.StreamingSink

/#/#定义上传数据流是否存在scheam

streaming.sinks.streamingSink.uploadType=false

/#/#定义用户身份标识

streaming.sinks.streamingSink.appKey=＜your app key＞

streaming.sinks.streamingSink.appSecret=＜your app secret key＞

streaming.sinks.streamingSink.streamingName=＜流总线topic名称＞

streaming.sinks.streamingSink.batchSize=100

streaming.sinks.streamingSink.serverUrl=[http://streamhub-gw.jcloud.com](http://streamhub-gw.jcloud.com/)

(1)公网地址：

华南:[http://streamhub-gw.jcloud.com](http://streamhub-gw.jcloud.com/)

华北:[http://hb-streamhub-gw.jcloud.com](http://hb-streamhub-gw.jcloud.com/)

(2)内网地址：

华南: streamhub-gw-inner.jcloud.com

华北: hb-streamhub-gw-inner.jcloud.com

**6. 定义source对应channel**

/#/#sourcechannel

streaming.sources.tailDirSrc.channels=memoryChannel

****

**7.****定义sink对应channel**

/#/#sinkchannel

streaming.sinks.streamingSink.channel=memoryChannel

**8.****启动Agent**

***注：启动Agent之前请确认已正确安装JDK并配置环境变量。***

在bin目录下执行如下命令：

./flume-ng agent -nstreaming -c conf -f ../conf/test.properties-Dflume.root.logger=INFO,LOGFILE,console

**Tips:****常见的内存OOM****问题解决方案**

****

首先限制JVM的内存使用，在flume的flume-env.sh配置文件中配置JVM参数

JAVA_OPTS="-Xms1000m -Xmx1000m"

这里的例子是配置1000M，可以根据对应的机器内存进行灵活配置，同时配合修改channel的capacity和transactionCapacity，如果自己的内存比较小，这里的参数也应设置的比较小，在配置完JVM的参数以后，启动agent时应加上-c conf 选项，否则配置不会生效。例如：bin/flume-ng agent -n streaming -c conf -f conf/flume-conf.properties -Dflume.root.logger=INFO,LOGFILE,console > faoling.log

另一种方案是channel的类型不使用内存，使用文件，使用文件的时候要比使用内存效率低，可以根据实际情况灵活使用，如果本机配置不高或者日志生成速度比较慢可以考虑使用。

****