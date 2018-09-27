# **volume ls**

Usage: jcloud volume ls [OPTIONS]
List volumes
-f, --filter=[] Provide filter values (i.e. 'dangling=true')
--help=false Print usage
-q, --quiet=false Only display volume names

列出京东云容器服务的所有硬盘。可以使用

-f
或

--filter
标志位来过滤。过滤的格式是一个

key=value
键值对。要指定多于一个的过滤器，可以传递多个标志位（例如，

--filter"foo=bar" --filter "bif=baz"
）。

只支持过滤器

dangling=value
，其值是

true
或

false
的布尔值。

输出示例：
$ jcloud volume create --name rose
rose
$ jcloud volume create --name tyler --size=50
tyler
$ jcloud volume ls
DRIVER VOLUME NAME SIZE CONTAINER
hyper rose 10g
hyper tyler 50g