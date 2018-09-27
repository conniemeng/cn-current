# **log****i****n******

Usage: jcloud login [OPTIONS] [SERVER]
Make Jcloud.com to log in to a Docker registry server, if no server is specified "https://index.docker.io/v1/" is the default.
-e, --email="" Email
--help=false Print usage
-p, --password="" Password
-u,--username="" Username

您可以登录到任何拥有鉴权证书并且可通过互联网访问的公共或私有镜像仓库。

登录成功后，该命令将授权证书保存在$

HOME/.jcloud/config.json
路径下。

注意：

1、未指定任何镜像仓库地址时，默认登录“https://index.docker.io/v1/";

2、当运行

sudo jcloud login
命令时，证书将被保存在

/root/.jcloud/config.json路径

下。