# **ps**

Usage: jcloud ps [OPTIONS]
List containers
-a, --all=false Show all containers (default shows just running)
-f, --filter=[] Filter output based on conditions provided
--format=[] Pretty-print containers using a Go template
--help=false Print usage
-l, --latest=false Show the latest created container (includes all states)
-n=-1 Show n last created containers (includes all states)
--no-trunc=false Don't truncate output
-q, --quiet=false Only display numeric IDs
-s, --size=false Display total file sizes

示例：

$ jcloud ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
4c01db0b339c ubuntu:12.04 bash 17 seconds ago Up 16 seconds 3300-3310/tcp webapp
d7886598dbe2 crosbymichael/redis:latest /redis-server --dir 33 minutes ago Up 33 minutes 6379/tcp redis,webapp/db

默认情况下，

jcloud ps
命令仅显示正在运行的容器。要查看全部容器，使用：

jcloud ps -a
命令。

jcloud ps
命令会尽量将暴露的端口分组到一个范围内。例如，一个暴露TCP端口

100, 101, 102
的容器会在

PORTS
那一列中显示

100-102/tcp
。

备注：运行

jcloud ps --no-trunc
命令可以显示两个链接在一起的容器。

## **Filtering**

过滤标志（

-f
或

--filter

）
的格式是一个

key=value
键值对。如果有多个过滤器，则传递多个标志位（例如，

--filter"foo=bar" --filter "bif=baz"
）。

目前支持的过滤器有：

* 
id (容器id)
* 
label (

label=
或

label==
)
* 
name (容器名称)
* 
exited (int - 退出容器的代码。仅用于

--all
)
* 
status (创建|重启|运行|暂停|退出)
* 
ancestor (

[:]
, 或 ) - 由给定镜像或其子镜像创建的过滤器容器

## **Label**

label
过滤器基于标签本身或标签及其对应值来匹配容器。

以下过滤器使用

color
标签对容器进行匹配，未匹配标签值：
$ jcloud ps --filter "label=color"
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
673394ef1d4c busybox "top" 47 seconds ago Up 45 seconds nostalgic-shockley
d85756f57265 busybox "top" 52 seconds ago Up 51 seconds high-albattani

以下过滤器使用color标签和blue标签值来匹配容器。

$ jcloud ps --filter "label=color=blue"
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
d85756f57265 busybox "top" About a minute ago Up About a minute high-albattani

## **Name**

name
过滤器使用容器全名或部分名称来匹配肉弄过去。

以下过滤器将匹配名称包含

nostalgic-stallman
字符串的所有容器。
$ jcloud ps --filter "name=nostalgic-stallman"
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
9b6247364a03 busybox "top" 2 minutes ago Up 2 minutes nostalgic-stallman

也可以只筛选名称中的子字符串，如下：

$ jcloud ps --filter "name=nostalgic"
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
715ebfcee040 busybox "top" 3 seconds ago Up 1 seconds i-am-nostalgic
9b6247364a03 busybox "top" 7 minutes ago Up 7 minutes nostalgic-stallman
673394ef1d4c busybox "top" 38 minutes ago Up 38 minutes nostalgic-shockley

## **Exited**

exited
过滤器通过状态代码来匹配容器。例如，要筛选已成功退出的容器：
$ jcloud ps -a --filter 'exited=0'
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
ea09c3c82f6e registry:latest /srv/run.sh 2 weeks ago Exited (0) 2 weeks ago 127.0.0.1:5000->5000/tcp desperate-leakey
106ea823fe4e fedora:latest /bin/sh -c 'bash -l' 2 weeks ago Exited (0) 2 weeks ago determined-albattani
48ee228c9464 fedora:20 bash 2 weeks ago Exited (0) 2 weeks ago tender-torvalds

## **Status**

status
过滤器通过状态来匹配容器。可以使用

created
，

restarting
，

running
，

paused
和

exited
来进行过滤。例如，筛选出正在运行状态的容器：
$ jcloud ps --filter status=running
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
715ebfcee040 busybox "top" 16 minutes ago Up 16 minutes i-am-nostalgic
d5c976d3c462 busybox "top" 23 minutes ago Up 23 minutes top
9b6247364a03 busybox "top" 24 minutes ago Up 24 minutes nostalgic-stallman

筛选暂停状态的容器：

$ jcloud ps --filter status=paused
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
673394ef1d4c busybox "top" About an hour ago Up About an hour (Paused) nostalgic-shockley

## **Ancestor**

Ancestor过滤器基于容器的镜像或者其子镜像来匹配容器。该过滤器支持以下的镜像描述：

* 
image
* 
image:tag
* 
image:tag@digest
* 
short-id
* 
full-id

如果没有指定

tag
，则默认使用

latest
。例如：过滤使用

ubuntu
镜像最新版本的容器：
$ jcloud ps --filter ancestor=ubuntu
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
919e1179bdb8 ubuntu-c1 "top" About a minute ago Up About a minute admiring-lovelace
5d1e4a540723 ubuntu-c2 "top" About a minute ago Up About a minute admiring-sammet
82a598284012 ubuntu "top" 3 minutes ago Up 3 minutes sleepy-bose
bab2a34ba363 ubuntu "top" 3 minutes ago Up 3 minutes focused-yonath

匹配基于

ubuntu-c1
镜像的容器，该镜像是

ubuntu镜像的子镜像
：

$ jcloud ps --filter ancestor=ubuntu-c1
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
919e1179bdb8 ubuntu-c1 "top" About a minute ago Up About a minute admiring-lovelace

匹配基于12.04.5版本ubuntu镜像的容器：

$ jcloud ps --filter ancestor=ubuntu:12.04.5
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
82a598284012 ubuntu:12.04.5 "top" 3 minutes ago Up 3 minutes sleepy-bose

匹配基于

d0e008c6cf02
镜像层构建的容器或堆栈中包含此镜像层的镜像。

$ jcloud ps --filter ancestor=d0e008c6cf02
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
82a598284012 ubuntu:12.04.5 "top" 3 minutes ago Up 3 minutes sleepy-bose

## **Formatting**

格式化选项(

--format
) 会使用Go模板打印容器输出。

Go模板的有效占位符如下所示：
占位符

说明.ID

容器ID.Image

镜像ID.Command

引用命令.CreatedAt

容器创建时间.RunningFor

容器启动时长.Ports

暴露端口.Status

容器状态.Size

容器磁盘大小.Names

容器名称.Labels

分配给容器的全部标签.Label

容器指定标签的值

当使用

--format
选项时，

ps
命令将完全按照模板声明的方式输出数据，或使用

table
指令将列标头一起输出。

以下示例将使用不带标头的模板并输出用冒号“：”分隔开的所有正在运行的容器的ID与命令：
$ jcloud ps --format "{{.ID}}: {{.Command}}"
a87ecb4f327c: /bin/sh -c /#(nop) MA
01946d9d34d8: /bin/sh -c /#(nop) MA
c1d3b0166030: /bin/sh -c yum -y up
41d50ecd2f57: /bin/sh -c /#(nop) MA

以表格格式列出所有正在运行的容器及其标签：

$ jcloud ps --format "table {{.ID}}\t{{.Labels}}"
CONTAINER ID LABELS
a87ecb4f327c com.docker.swarm.node=ubuntu,com.docker.swarm.storage=ssd
01946d9d34d8
c1d3b0166030 com.docker.swarm.node=debian,com.docker.swarm.cpu=6
41d50ecd2f57 com.docker.swarm.node=fedora,com.docker.swarm.cpu=3,com.docker.swarm.storage=ss