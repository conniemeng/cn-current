# **pull**

Usage: jcloud pull [OPTIONS] NAME[:TAG] | [REGISTRY_HOST[:REGISTRY_PORT]/]NAME[:TAG]
Pull an image or a repository from the registry
--disable-content-trust=true Skip image verification
--help=false Print usage

[Docker Hub](https://hub.docker.com/explore/)镜像仓库为您构建自己的镜像提供基础镜像。基础镜像位于镜像层的最下层。

[Docker Hub](https://hub.docker.com/explore/)中有很多预构建镜像，你可以拉取镜像来尝试创建不需要定义的镜像。

也可以手动指定拉取镜像的仓库路径。例如，如果你构建了本地镜像仓库，你可以从本地镜像库中拉去镜像。存储库路径与URL类似，但不包含协议说明符（例如，https://）。

下载特定镜像或者一组镜像（即存储库），使用 jcloud pull命令：

$ jcloud pull debian
/# will pull the debian:latest image and its intermediate layers
$ jcloud pull debian:testing
/# will pull the image named debian:testing and any intermediate
/# layers it is based on.
$ jcloud pull debian@sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf
/# will pull the image from the debian repository with the digest
/# sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf
/# and any intermediate layers it is based on.
/# (Typically the empty `scratch` image, a MAINTAINER layer,
/# and the un-tarred base).
$ jcloud pull registry.hub.docker.com/debian
/# manually specifies the path to the default Docker registry. This could
/# be replaced with the path to a local registry to pull from another source.
/# sudo jcloud pull myhub.com:8080/test-image

jcloud pull
命令在终端正在运行时，通过按

CTRL-c
来停止镜像拉取将不会终止镜像拉取操作。