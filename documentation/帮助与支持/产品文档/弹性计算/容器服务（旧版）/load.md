# **load**

Usage:jcloud load [OPTIONS]
Load an image from a tar archive
--help Print usage
-i, --input Read from a remote archive file compressed with gzip, bzip, or xz
-q, --quiet Do not show load process

上传tar格式的本地镜像。

注意：

1、暂不支持从本地同时加载多个镜像；

2、镜像文件最大不能超过4GB。

示例：

从公共URL导入镜像：
$ jcloud load -i http://<bucket>.oss.cn-north-1.jcloudcs.com/helloworld.tar

以静默模式导入镜像：

$ jcloud load -q -i http://<bucket>.oss.cn-north-1.jcloudcs.com/helloworld.tar

从压缩文件导入镜像：

$ jcloud load -i http://<bucket>.oss.cn-north-1.jcloudcs.com/helloworld.tar.gz

导入多个镜像：

$ jcloud load -i http://<bucket>.oss.cn-north-1.jcloudcs.com/busybox_alpine.tar

从s3 pre-signed URL导入镜像：

$ jcloud load -i https://<bucket>.s3-us-west-1.amazonaws.com/private/cirros.tar?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIxxxxxxxxxxxxxxx%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20160523T120846Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Signature=0eb3a3777cdc633f1bb0c05de0b950eb9bd560696eb5cffd26b493e1ea1a4fb0

通过基本认证载入镜像：

$ jcloud load -i http://<username>:<password>@<host_domain>/helloworld.tar