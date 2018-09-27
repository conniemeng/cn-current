# **create**

Usage: jcloud create [OPTIONS] IMAGE [COMMAND] [ARG...]
Create a new container
-a, --attach=[] Attach to STDIN, STDOUT or STDERR
--cidfile Write the container ID to the file
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
--name Assign a name to the container (max length: 48)
--noauto-volume Do not create volumes specified in image
-P, --publish-all Publish all exposed ports
-p, --publish=[] Publish a container's port(s)
--protection=false Termination protection for container
--restart=no Restart policy to apply when a container exits
--sg=[] Security group for each container
--size=s4 The type for each instance (e.g. s1, s2, s3, s4, m1, m2, m3, l1, l2, l3)
--stop-signal=SIGTERM Signal to stop a container, SIGTERM by default
-t, --tty Allocate a pseudo-TTY
-v, --volume=[] Bind mount a volume
-w, --workdir Working directory inside the container

****

jcloud create
命令将在指定的镜像上创建一个可写的容器层，完成相应的配置环境，并将容器的ID输出到

STDOUT
。 与

jcloud run -d
命令类似，但jcloud create命令只创建但不启动容器，可以使用

jcloud start <container_id>
命令启动容器。

jcloud create可以提前完成容器配置，并将容器状态初始化为“Created”状态。

请查看[run运行命令](http://www.jcloud.com/help/detail/629/isCateLog/1)部分来获取更多详情。

## **示例**

$ jcloud create -t -i fedora bash
6d8af538ec541dd581ebc2a24153a28329acb5268abe5ef868c1f1a261221752
$ jcloud start -a -i 6d8af538ec5
bash-4.2/#

执行jcloud create命令时，也对硬盘执行初始化操作
（适用于

jcloud run
）；使用jcloud create创建一个容器和一块硬盘，在另外一个容器中对硬盘执行读写操作，参考示例：

$ jcloud create -v /data --name data ubuntu
240633dfbb98128fa77473d3d9018f6123b99c454b3251427ae190a7d951ad57
$ jcloud run --rm ubuntu ls -la /data
total 8
drwxr-xr-x 2 root root 4096 Dec 5 04:10 .
drwxr-xr-x 48 root root 4096 Dec 5 04:11 ..