# **stats**

Usage: jcloud stats [OPTIONS] [CONTAINER...]
Display a live stream of container(s) resource usage statistics
-a, --all Show all containers (default shows just running)
--help Print usage
--no-stream Disable streaming stats and only pull the first result

jcloud stats
命令会返回运行容器的实时数据流。通过指定由空格分隔的容器的名称或id的列表，可以将数据限制为一到多个特定容器。你可以指定一个已停止的容器，但是已停止的容器不会返回任何数据。

如果你想了解有关容器资源使用情况的更多详细信息，请使用

/containers/(id)/stats
API。

示例

在所有正在运行的容器上运行

jcloud stats
命令：
$ jcloud stats
CONTAINER CPU % MEM USAGE / LIMIT MEM % NET I/O BLOCK I/O
1285939c1fd3 0.07% 796 KB / 64 MB 1.21% 788 B / 648 B 3.568 MB / 512 KB
9c76f7834ae2 0.07% 2.746 MB / 64 MB 4.29% 1.266 KB / 648 B 12.4 MB / 0 B
d1ea048f04e4 0.03% 4.583 MB / 64 MB 6.30% 2.854 KB / 648 B 27.7 MB / 0 B

按名称或ID在多个容器上运行

jcloud stats
命令：

$ jcloud stats fervent-panini 5acfcb1b4fd1
CONTAINER CPU % MEM USAGE/LIMIT MEM % NET I/O
5acfcb1b4fd1 0.00% 115.2 MB/1.045 GB 11.03% 1.422 kB/648 B
fervent-panini 0.02% 11.08 MB/1.045 GB 1.06% 648 B/648 B