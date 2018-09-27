# **run**

Usage: jcloud run [OPTIONS] IMAGE [COMMAND] [ARG...]
Run a new container
-a, --attach=[] Attach to STDIN, STDOUT or STDERR
--cidfile Write the container ID to the file
-d, --detach Run container in background and print container ID
--disable-content-trust=true Skip image verification
-e, --env=[] Set environment variables
--entrypoint Overwrite the default ENTRYPOINT of the image
--env-file=[] Read in a file of environment variables
--expose=[] Expose a port or a range of ports
-h, --hostname Container host name
--help Print usage
-i, --interactive Keep STDIN open even if not attached
-l, --label=[] Set meta data on a container
--label-file=[] Read in a line delimited file of labels
--link=[] Add link to another container
--name Assign a name to the container
--noauto-volume Do not create volumes specified in image
-P, --publish-all Publish all exposed ports
-p, --publish=[] Publish a container's port(s)
--protection=false Termination protection for container
--restart=no Restart policy to apply when a container exits
--rm Automatically remove the container when it exits
--sg=[] Security group for each container
--size=s4 The type for each instance (e.g. s1, s2, s3, s4, m1, m2, m3, l1, l2, l3)
--stop-signal=SIGTERM Signal to stop a container, SIGTERM by default
-t, --tty Allocate a pseudo-TTY
-v, --volume=[] Bind mount a volume
-w, --workdir Working directory inside the container

jcloud run
命令首先在指定镜像上创建一个可写的容器层，然后使用指定的容器镜像来启动它。也就是说，

jcloud run
命令相当于先执行

/container/create命令
然后执行

/container/(id)/start命令
。使用

jcloud start
命令可以重新启动已经停止的容器，并保证原有修改项的完整性。请参见[
jcloud ps
](https://www.jcloud.com/help/detail/623/isCateLog/1)

-a
命令来查看所有容器的列表。

## **示例**

**设置工作目录（-w）**
$ jcloud run -w /path/to/dir/ -i -t ubuntu pwd

-w
参数允许在指定目录中执行命令，以这里

/path/to/dir/
为例，如果路径不存在，则在容器内创建该路径。

注意：当容器中只有一个Docker镜像时，该参数才有效。

**挂载云硬盘（-v）**
$ jcloud run -d -v hello:/world busybox ls /world

发生挂载在容器中的

/world
目录下。京东云容器不支持容器内挂载点的相对路径。

**设置环境变量（-e，--env，--env-file）**
$ jcloud run -e MYVAR1 --env MYVAR2=foo --env-file ./env.list ubuntu bash

该命令会设置容器内的环境变量。这里将对三个标志进行说明。其中

-e
，

--env
参数会取环境变量及其值，如果没有

=
，则传递该变量的当前值（中主机比如的

$MYVAR1
值被设置为容器中

$MYVAR1
的值）当然没有

=
并且该变量没有在客户端环境中定义时，该变量将会从容器的环境变量列表中被删除所有的三个标志位

-e
，

--env
和

--env-file
都可以重复使用。

无论这三个标志位的顺序如何，处理首先

--env-file
标志位，然后处理

-e
，

--env
标志位。这样，

-e
或

--env
标志位可以根据需求覆盖变量。
$ cat ./env.list
TEST_FOO=BAR
$ jcloud run --env TEST_FOO="This is a test" --env-file ./env.list busybox env | grep TEST_FOO
TEST_FOO=This is a test

--env-file
位标志采用文件名作为参数并且期望每一行都处于

VAR=VAL
格式，模拟来传递给

--env
的参数。注释行只需在前缀标明

/#

使用

--env-file
传递的文件示例。
$ cat ./env.list
TEST_FOO=BAR
/# this is a comment
TEST_APP_DEST_HOST=10.10.0.127
TEST_APP_DEST_PORT=8888
_TEST_BAR=FOO
TEST_APP_42=magic
helloWorld=true
123qwe=bar
org.spring.config=something
/# pass through this variable from the caller
TEST_PASSTHROUGH
$ TEST_PASSTHROUGH=howdy jcloud run --env-file ./env.list busybox env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=5198e0745561
TEST_FOO=BAR
TEST_APP_DEST_HOST=10.10.0.127
TEST_APP_DEST_PORT=8888
_TEST_BAR=FOO
TEST_APP_42=magic
helloWorld=true
TEST_PASSTHROUGH=howdy
HOME=/fonte=bar
org.spring.config=something
$ jcloud run --env-file ./env.list busybox env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=5198e0745561
TEST_FOO=BAR
TEST_APP_DEST_HOST=10.10.0.127
TEST_APP_DEST_PORT=8888
_TEST_BAR=FOO
TEST_APP_42=magic
helloWorld=true
TEST_PASSTHROUGH=
HOME=/root
123qwe=bar
org.spring.config=something

**暴露传入端口**

除了

EXPOSE
指令外，镜像开发人员对网络没有太多的控制。

EXPOSE
指令定义了提供服务的初始入站端口。这些端口可应用于容器内的进程。员操作柯林斯使用

--expose
选项对话添加暴露端口。

默认情况下，即使给容器附加一个FIP，容器的暴露端口也只能由用户的容器进行访问。人员操作启动在容器时使用

-P
或

-p
标志位，可以将容器的内部端口发布为公众。这个发布的端口可以被任何能访问容器的客户端所访问到。
--expose=[]: Expose a port or a range of ports inside the container.
These are additional to those exposed by the `EXPOSE` instruction
-P : Publish all exposed ports to public
-p=[] : Publish a container᾿s port or a range of ports to public
format: exposedPort:containerPort
Both exposedPort and containerPort can be specified as a
range of ports. When specifying ranges for both, the
number of container ports in the range must match the
number of host ports in the range, for example:
-p 1234-1236:1234-1236/tcp
When specifying a range for exposedPort only, the
containerPort must not be a range. In this case the
container port is published somewhere within the
specified hostPort range. (e.g., `-p 1234-1236:1234/tcp`)

注意：发布端口的最大值为32。

**设置容器元数据（-l，--label，--label-file）**

标签是将元数据应用于容器的

key=value
。键值对为具有两个标签的容器添加标签：
$ jcloud run -l my-label --label com.example.foo=bar ubuntu bash

my-label
键未指定值，因为该标签的默认值为空字符串（

""
）。可以重复的使用标签标志位（

-l
或

--label
）来添加多组标签。

key=value
键值对必须是唯一的，以避免覆盖标签值。如果要指定键值相同而标签值不同的标签，则后续的每一个值都将覆盖前一个。云京东容器将使用你提供的求最后一个

key=value
键值对。

使用

--label-file
标志位从文件加载多个标签使用EOL标记为文件中的每个标签进行分隔下面的示例会从当前目录的标签文件加载标签。：
$ jcloud run --label-file ./labels ubuntu bash

（与环境变量不同的是，标签对于运行在容器内的进程是不可见的。）以下示例对标签文件格式进行了说明：

com.example.label1="a label"
/# this is a comment
com.example.label2=another\ label
com.example.label3

可以你通过提供多个

--label-file
标志位来加载对个标签文件。

**关联到TDIN / STDOUT / STDERR（-a）**

-a
位标志将

jcloud run
命令绑定到容器的

STDIN
，

STDOUT
或

STDERR
。这使得按照需求来控制输出和输入是有可能的。
$ echo "test" | jcloud run -i -a stdin ubuntu cat -

该命令将数据导入容器，通过并仅展示进入容器的

STDIN
来打印容器的ID。

$ jcloud run -a stderr ubuntu echo test

该命令没有错误发生时不会打印任何内容，因为我们仅进入了容器的

STDERR
。的容器日志仍然存储写入到

STDERR
状语从句：

STDOUT
。

$ cat somefile | jcloud run -i -a stdin mybuilder dobuild

该命令将文件以管道形式导入可以被构建的容器。构建完成后将打印容器ID，容器而且构建的日志也。可以通过

jcloud logs
命令来检索。这对于向容器内导入文件或其他内容，并且可以在容器运行完成时立刻检索容器ID，十分有用。

**重启策略（--restart）**

京东使用云容器服务的

--restart
命令来指定容器的重启策略。重启策略控制的是容器退出后是否重启该容器。如果容器的正常运行时间超过10秒，则会触发重启策略。京东云容器服务支持以下重启策略：
策略

结果no

容器退出后不会自动重启该容器。默认情况。on-failure[：max-retries]

仅当容器以非零退出状态退出时容器容器。可选择限制重启的重试次数。always

无论容器的退出状态如何，始终重启容器。当你始终重启时，京东云容器服务会无限期的重启容器。容器也将始终在守护进程启动时启动，不考虑容器的当前状态。unless-stopped

无论退出状态是什么，总是重启容器，但是如果容器被设置为停止状态后，就不会在守护进程启动时启动该容器。$ jcloud run --restart=always redis

对名称为

redis
的容器执行always重启策略。如果该容器退出，京东云容器服务会重启容器。

**添加安全组（--sg）**

--sg
位标志会告诉

京东云容器服务
命令给容器添加安全组。一个安全组可以控制一个或多个容器的数据传输，起着虚拟防火墙的作用。
$ jcloud run --sg ssh --sg web -d jdeathe/centos-ssh

注意：

ssh
状语从句：

web
的英文与新容器相关的安全组的名称。

**无自动镜像存储盘（--noauto-volume）**

--noauto-volume
参数设置后，京东云容器服务将不会为容器创建镜像存储盘。如未设置该参数，hyper run将自动为容器创建一个镜像存储盘。
$ jcloud run --noauto-volume image-with-volume

**开启终止保护（ -- protection）**

--protection
参数将为容器开启终止保护。取消终止保护前，容器不允许被删除，您可以使用

jcloud update --protection=false <container>命令取消指定容器的终止保护状态
。
$ jcloud run --protection=true busybox