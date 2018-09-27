# **rm**

Usage: jcloud rm [OPTIONS] CONTAINER [CONTAINER...]
Remove one or more containers
-f, --force=false Force the removal of a running container (uses SIGKILL)
--help=false Print usage
-v, --volumes=false Remove auto-created volumes associated with the container

示例

$ jcloud rm /redis
/redis

删除在

/redis
所代表的容器。

$ jcloud rm --link /webapp/redis
/webapp/redis

删除

/webapp
和

/redis
容器之间的底层链接，删除所有网络通信。

$ hype rm --force redis
redis

给

/redis
所代表的容器中的主进程发送

SIGKILL
，然后删除容器。