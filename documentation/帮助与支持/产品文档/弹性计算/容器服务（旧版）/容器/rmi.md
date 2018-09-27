# **rmi**

Usage: jcloud rmi [OPTIONS] IMAGE [IMAGE...]
Remove one or more images
-f, --force=false Force removal of the image
--help=false Print usage

你可以使用镜像的短ID ，长ID ，标签或摘要来删除镜像。如果一个镜像有多个标签或摘要引用，你必须在删除该镜像之前将它们全部删除。

$ jcloud images
REPOSITORY TAG IMAGE ID CREATED SIZE
test1 latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
test latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
test2 latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
$ jcloudr rmi fd484f19954f
Error: Conflict, cannot delete image fd484f19954f because it is tagged in multiple repositories, use -f to force
2013/12/11 05:47:16 Error: failed to remove one or more images
$ jcloud rmi test1
Untagged: test1:latest
$ hyper rmi test2
Untagged: test2:latest
$ jcloud images
REPOSITORY TAG IMAGE ID CREATED SIZE
test latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
$ jcloud rmi test
Untagged: test:latest
Deleted: fd484f19954f4920da7ff372b5067f5b7ddb2fd3830cecd17b96ea9e286ba5b8

如果你使用

-f
标志位并且指定镜像的短ID 或长ID ，该命令会对所有与指定ID 匹配的镜像取消标记并删除它。

$ jcloud images
REPOSITORY TAG IMAGE ID CREATED SIZE
test1 latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
test latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
test2 latest fd484f19954f 23 seconds ago 7 B (virtual 4.964 MB)
$ jcloud rmi -f fd484f19954f
Untagged: test1:latest
Untagged: test:latest
Untagged: test2:latest
Deleted: fd484f19954f4920da7ff372b5067f5b7ddb2fd3830cecd17b96ea9e286ba5b8

通过digest 拉取的镜像没有与其相关联的标签：

$ jcloud images --digests
REPOSITORY TAG DIGEST IMAGE ID CREATED VIRTUAL SIZE
localhost:5000/test/busybox <none> sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf 4986bf8c1536 9 weeks ago 2.43 MB

通过摘要删除镜像：

$ jcloud rmi localhost:5000/test/busybox@sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf
Untagged: localhost:5000/test/busybox@sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf
Deleted: 4986bf8c15363d1c5d15512d5266f8777bfba4974ac56e3270e7760f6f0a8125
Deleted: ea13149945cb6b1e746bf28032f02e9b5a793523481a0a18645fc77ad53c4ea2
Deleted: df7546f9f060a2268024c8a230d8639878585defcc1bc6f79d2728a13957871b