# **fip release**

Usage: jcloud fip release [OPTIONS] IP [IP...]
Release a fip
--help=false Print usage

释放一个或多个Floating IP

$ jcloud fip release 211.98.26.102
211.98.26.102

要释放的Floating IP不能与任何容器连接。否则京东云容器服务报错：

$ jcloud fip release 211.98.26.102
211.98.26.102 is in use