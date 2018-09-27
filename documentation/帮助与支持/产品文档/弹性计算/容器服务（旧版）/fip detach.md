# **fip detach**

Usage: jcloud fip detach [OPTIONS] CONTAINER
--help=false Print usage

将 fip 从容器中解绑：

$ jcloud fip detach myweb
211.98.26.102

如果对没有 fip 的容器执行解绑 fip 操作，京东云容器服务会报错：

$ jcloud fip detach myweb
No floating IP attached