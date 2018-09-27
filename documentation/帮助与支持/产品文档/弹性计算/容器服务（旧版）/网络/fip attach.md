# **fip attach**

Usage: jcloud fip attach [OPTIONS] FIP CONTAINER
Attach floating IP to a (running) container
--help=false Print usage

将分配的Floating IP连接到（正在运行的）容器上：

$ jcloud fip attach 211.98.26.102 myweb
myweb

如果尝试将Floating IP连接到没有在运行的容器上，京东云容器服务会返回错误：

$ jcloud fip attach 211.98.26.102 myweb
myweb is not running

每个容器只能有一个Floating IP。如果尝试给容器附加另一个Floating IP，会返回错误：

$ jcloud fip attach211.98.26.102 myweb