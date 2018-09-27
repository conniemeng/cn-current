# **Compose文件说明**

Compose 使用YAML文件定义服务、网络和云硬盘。Compose文件的缺省路径是 ./docker-compose.yml。

服务定义包含了该服务启动的每一个容器所需的配置信息，类似在命令行运行[jcloud run](https://www.jcloud.com/help/detail/629/isCateLog/1)时需要设置参数。同样，网络和云硬盘的定义类似于执行 [jcloud fip attach](https://www.jcloud.com/help/detail/646/isCateLog/1) 和 [jcloud volume create](https://www.jcloud.com/help/detail/638/isCateLog/1)。

和[jcloud run](https://www.jcloud.com/help/detail/629/isCateLog/1) 一样，Docker镜像中指定的命令（如 CMD，EXPOSE，VOLUME，ENV）将默认被执行，也就是说，不需要在 docker-compose.yml 中再次定义。

你可以在配置变量中定义环境变量，采用 Bash 语法格式 ${VARIABLE}。

****

**服务配置说明**

jcloud compose 只支持两个版本的 Compose 格式 - version 1（是传统格式，不支持云硬盘和网络）和version 2。

**command**

重写默认指令
command: bundle exec thin -p 3000

命令可以指定多个参数

command: [bundle, exec, thin, -p, 3000]

**container name******

设置自定义的容器名称，而不是自动生成的缺省名称。
container_name: my-web-container

由于京东云的容器名称是唯一的，所以如果你指定了一个自定义的名称，你就无法将服务扩容至多台容器，否则会导致出错。

**depends_on**

描述服务之间的依赖关系，有以下两种效果：

* 
compose up 会根据依赖的顺序启动服务。在下面的例子当中，db 和redis启动后才会启动web。
* 
compose up SERVICE 会自动包含 SERVICE 的依赖。在下面的例子中，jcloud compose up web 将会创建并启动 db和redis。

## **示例**

version: '2'
services:
web:
image: wordpress
depends_on:
- db
db:
image: mysql

注意：depends_on 在db和redis启动后就会启动web，不会等到 db 和redis处于“ready”状态再启动 web。如果需要实现等待服务处于 ready 状态，可以查看控制启动顺序部分了解详情。

**entrypoint**

重写默认 entrypoint 命令：
entrypoint: /code/entrypoint.sh

entrypoint 命令可以包含多个参数：

entrypoint:
- php
- -d
- zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so
- -d
- memory_limit=-1
- vendor/bin/phpunit

**env_file**

从文件中添加环境变量，多个文件使用列表格式设置。如果你已经使用 compose -f FILE 命令指定了Compose 文件，那么 env_file 中的文件路径是Compose 文件所在文件夹的相对路径，并且env_file设置的环境变量将会重写Compose 文件中指定的环境变量。

env_file:
- ./common.env
- ./apps/web.env
- /opt/secrets.env

env文件中的每一行都使用 VAR=VAL格式定义。以/#（即注释）开头的行为注释行，执行compose命令时将会被忽略。

/# Set Rails/fontonment
RACK_ENV=development

**environment**

可以使用数组或映射表形式来添加环境变量。任何布尔类型的数值 true、false、yes、no 都必须用双引号括起来，否则将会被 YAML 编译器转换成True 或者 False。对于只包含一个键值的环境变量，其对应值将从 Compose 运行的机器上获取，适用于私有或宿主机专用数据值。

environment:
RACK_ENV: development
SHOW: 'true'
SESSION_SECRET:
environment:
- RACK_ENV=development
- SHOW=true
- SESSION_SECRET

**extends**

在当前文件或其他文件中扩展一个新服务，可以选择是否覆盖配置信息。在任何服务中，你都可以使用 extends 命令扩展服务，并设置不同的配置。Extends 的值必须是一个定义了服务及其可选关键字 的映射表。

extends:
file: common.yml
service: webapp

正在被扩展的服务名称，比如 web 或者数据库。File 值表示定义了该服务的 Compose 配置文件的位置信息。如果你没有指定 file 这个关键字，那么 Compose 将会在当前目录寻找 service 的配置文件。file 的值可以是绝对路径或者相对路径。如果指定相对路径，则 Compose 将其视为相对于当前文件夹的相对路径。此外，可以扩展一个本身就扩展了其他服务的服务，而且可以无限期地扩展。Compose 不支持循环引用，如果 Compose 遇到循环引用则返回错误。

**external_links**

用于链接那些没有在 docker-compose.yml 重定义，甚至没有使用 Compose 命令启动，特别是对于提供共享或公共服务的容器。当同时指定容器名称和链接别名（CONTAINER：ALIAS）时，external_links遵循类似于links的语义。

external_links:
- redis_1
- project_db_1:mysql
- project_db_1:postgresql

注意：如果你正使用的是版本二的文件格式，那么与外部创建的容器连接的所有容器服务中，必须存在一个容器服务和外部创建的容器处于相同的网络。

**image**

指定启动容器时开始的镜像，这个镜像可以的值可以是 repository/tag 或者是镜像的 ID。

image: redis
image: ubuntu:14.04
image: tutum/influxdb
image: example-registry.com:4000/postgresql
image: a4bc65fd

如果镜像不存在，Compose 会尝试从镜像库中拉取，除非你指定了特定的镜像版本，那么它就使用指定的指令构建它，并用指定的标签标记它。

**labels**

使用京东云容器服务标签向容器添加元数据。你可以使用数组或字典，建议使用反向DNS符号来防止你的标签与其他软件使用的标签冲突。

labels:
com.example.description: "Accounting webapp"
com.example.department: "Finance"
com.example.label-with-empty-value: ""
labels:
- "com.example.description=Accounting webapp"
- "com.example.department=Finance"
- "com.example.label-with-empty-value"

**links**

链接到另一个服务中的容器。需要指定服务名称和链接别名（SERVICE：ALIAS），或者仅指定服务名称。

web:
links:
- db
- db:database
- redis

如果服务的名称未指定别名，则可以在与别名相同的主机名或服务名称处访问链接服务的容器。Links以与depends_on相同的方式表示服务之间的依赖关系，因此它们决定了服务启动的顺序。

**volumes**

挂载路径或命名云硬盘。对于版本二的文件，云硬盘的名称可以使用最上层的卷的关键字、公共 http / https 源文件或公共 git 仓库。当使用版本一时，如果云硬盘不存在，京东云容器服务将自动创建一块新的云硬盘，名称就以输入的那个。

volumes:
/# Just specify a path and let the Engine create a volume
- /var/lib/mysql
/# Named volume, datavolume is volume name
- datavolume:/var/lib/my
/# Named volume, https source
- https://raw.githubusercontent.com/msanand/docker-workflow/master/node/Dockerfile:/data/Dockerfile
/# Named volume, git repository
- https://github.com/jcloudhq/jcloudcli.git:/data/jcloudcli

**fip**

将分配的 fip 附加到（正在运行的）容器上，每个容器只能有一个 fip。 它只接受一个单独的字符串：
fip: 211.98.26.102

**size**

每个容器的大小，它只接受一个单独的字符串。 可用的容器大小为 s1，s2，s3，s4，m1，m2，m3，l1，l2 和 l3。
size: s4

**noauto_volume**

这个指令指示京东云容器服务不要在容器镜像中为 VOLUME 字段创建新的云硬盘。如果未指定，则 Compose 将自动为容器镜像中的每个 VOLUME 字段创建云硬盘。
noauto_volume: true

**security_groups**

此指令指示compose向容器添加安全组。安全组充当控制一个或多个容器的流量的虚拟防火墙的角色。

security_groups:
- sg-test-1

**Jcloud compose vs Docker compose**

标签

docker compose

jcloud compose

详情Build

是

否cap_add

是

否

增加容器容量cap_drop

是

否

减少容器容量Command

是

是

覆盖缺省的命令cgroup_parent

是

否

为容器指定可选的父cgroupcontainer_name

是

是

指定自定义容器名称，而不是生成的缺省名称Devices

是

否

设备映射列表depends_on

是

是

表现服务之间的依属关系.dns

是

否

自定义DNS服务器，可以是单个值或列表dns_search

是

否

自定义DNS搜索域，可以是单个值或列表tmpfs

是

否

在容器中安装临时文件系统entrypoint

是

是

覆盖默认入口点.env_file

是

是

从文件中添加环境变量environment

是

是

添加环境变量expose

是

是

公开端口而不将其发布到主机（以后支持）extends

是

是

在当前文件或另一个文件中扩展另一个服务，可选地覆盖配置文件external_links

是

是

链接到在docker-compose.yml甚至Compose外部启动的容器extra_hosts

是

否

添加主机名映射image

是

是

指定容器开始启动时的镜像labels

是

是

使用Docker标签向容器添加元数据links

是

是

链接到另一个服务中的容器logging

是

否

记录服务的配置log_driver

是

否

指定日志驱动程序log_opt

是

否

将记录选项指定为键值对net

是

否

[仅版本一]网络模式network_mode

是

否

[仅版本二]网络模式networks

是

否

[仅版本二]要加入的网络aliases

是

否

网络上此服务的别名（备用主机名）ipv4_address

是

否

在加入网络时为此服务的容器指定静态IP地址ipv6_address

是

否

在加入网络时为此服务的容器指定静态IP地址pid

是

否

将PID模式设置为主机PID模式ports

是

是

公开端口security_opt

是

否

覆盖每个容器的默认标签方案stop_signal

是

是

设置停止容器的备用信号ulimits

是

否

覆盖容器的默认ulimitsvolumes

是

是

装载路径或命名数据卷volume_driver

是

否volume_from

是

否

从其他服务或容器装载所有数据卷cpu_shares

是

否

cpu_shares: 73cpu_quota

是

否

cpu_quota: 50000cpuset

是

否

cpuset: 0,1domainname

是

是

域名：foo.comhostname

是

是

主机名：booipc

是

否mac_address

是

否

Mac地址：02:42:ac:11:65:43mem_limit

是

否memswap_limit

是

否privileged

是

否read_only

是

否restart

是

是

总是重启shm_size

是

否stdin_open

是

是tty

是

是user

是

否working_dir

是

是size

否

是

京东云容器的实例大小fip

否

是

浮动IPsecurity_groups

否

是

安全组noauto_volume

否

是

不自动创建数据卷Volume configuration

是

是Network configuration

是

否