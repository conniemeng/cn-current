# **snapshot ls**

Usage: jcloud snapshot ls [OPTIONS]
List snapshots
--help=false Print usage
-q, --quiet=false Only display snapshot names

输出示例：

$ jcloud snapshot create --volume dbvol --name rose
rose
$ jcloud snapshot create --volume dbvol --name tyler
tyler
$ jcloud snapshot ls
Snapshot Name Volume Size
rose dbvol 20
tyler dbvol 20