# **compose rm**

Usage: jcloud compose rm [OPTIONS] [SERVICE...]
Remove stopped service containers.
--help Print usage
-p, --project-name Specify an alternate project name
-v Remove volumes associated with containers

注意：默认情况下，项目名称是当前目录的名称。如果没有正在运行的容器，则会删除compose项目。