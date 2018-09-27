# **volume rm**

Usage: jcloud volume rm [OPTIONS] VOLUME [VOLUME...]
Remove a volume
--help=false Print usage

删除一个或多个硬盘。已挂载到容器的硬盘不能被删除。

$ jcloud volume rm hello
hello