# **compose down**

****
Usage:jcloud compose down [OPTIONS]
Stop and remove containers, images, and volumes
created by `up`. Only containers and networks are removed by default.
--help Print usage
-p, --project-name Specify an alternate project name
--remove-orphans Remove containers for services not defined in the Compose file
--rmi Remove images, type may be one of: 'all' to remove
all images, or 'local' to remove only images that
don't have an custom name set by the `image` field
-v, --volumes Remove data volumes

注意：默认情况下，项目名称是当前目录的名称。

京东云容器服务的撰写不接受撰写文件，通过可以使用

-p
选项对话来操作项目。