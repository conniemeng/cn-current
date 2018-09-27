# **logout**

Usage: jcloud logout [SERVER]
Make Jcloud.com to log out from a Docker registry, if no server is specified "https://index.docker.io/v1/" is the default.
--help=false Print usage

退出镜像仓库登录状态。未指定镜像仓库地址时，默认退出“https://index.docker.io/v1/”仓库的登录状态。

例如：
$ jcloud logout