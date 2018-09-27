# **logs**

Usage: jcloud logs [OPTIONS] CONTAINER
Fetch the logs of a container
-f, --follow=false Follow log output
--help=false Print usage
--since="" Show logs since timestamp
-t, --timestamps=false Show timestamps
--tail="all" Number of lines to show from the end of the logs

注意：此命令仅可用于具有

json-file
和

journald
日志记录驱动程序的容器。

1、jcloud logs
命令可以批量检索执行时出现的日志。

2、jcloud logs --follow
命令会持续从容器的

STDOUT
和

STDERR
中流式传输新的输出。

3、如果为--tail参数设置负数或非整数，则参数值无效并将默认被重置为

all
。

4、jcloud logs --timestamps
指令会添加一个RFC3339Nano时间戳，例如每一条日志都有一个

2014-09-16T06:17:46.000000000Z
时间戳。在必要的情况下，为了确保时间戳能够对齐，时间戳中的纳秒级部分会被0填充。

5、设置

--since
参数后，将只输出指定日期后生成的容器日志。你可以将参数值设置为RFC 3339日期、UNIX时间戳或者Go语言的持续时间字符串(比如

1m30s
,

3h
)。除了RFC 3339日期格式，还可以使用RFC3339Nano格式，例如

2006-01-02T15:04:05
,

2006-01-02T15:04:05.999999999
,

2006-01-02Z07:00
, 和

2006-01-02
。如果你没有在时间戳的结尾使用z或者

+-00:00设置
时区偏移，将使用客户端的本地时区作为时间戳。当使用Unix时间戳计时时，这里的时间指的是从1970年1月1日开始流逝的秒数，而不是闰秒（又称Unix新纪元或Unix时间）。.nanoseconds是秒数的小数部分，且长度不超过9位。--since选项可以与

--follow
和

--tail
参数组合使用。