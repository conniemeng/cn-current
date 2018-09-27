# **fip ls**

Usage: jcloud fip ls [OPTIONS]
List snapshots
-f, --filter=[] Provide filter values (i.e. 'dangling=true')
--help=false Print usage
-q, --quiet=false Only display floating ip addresses

列出Jcloud的所有Floating IP。可以使用 -f 或 --filter 标志位来过滤。过滤的格式是一个 key=value键值对。
只支持过滤器dangling=value，其值是 true 或 false的布尔值。
示例输出：

$ jcloud fip ls
Floating IP Name Container Service
211.98.26.102
211.98.26.104 aa733d1782c92f295ff7291817b92c37938274b5e9fc3f4202c13f2db246192b
211.98.26.103 http