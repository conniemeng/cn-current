# **exec**

Usage: jcloud exec [OPTIONS] CONTAINER COMMAND [ARG...]
Run a command in a running container
-d, --detach=false Detached mode: run command in the background
--help=false Print usage
-t, --tty Allocate a pseudo-TTY
-i, --interactive=false Keep STDIN open even if not attached

jcloud exec
命令可以在正在运行的容器里运行一条新命令。

## **示例**

$ jcloud run --name ubuntu-bash --rm -i -t ubuntu bash

创建一个名为

ubuntu-bash
的容器并且启动一个Bash会话。

$ jcloud exec -d ubuntu-bash touch /tmp/execWorks

后台在运行的容器

ubuntu-bash
中创建一个缺省容器的新文件

/tmp/execWorks

。

$ jcloud exec -it ubuntu-bash bash

在

ubuntu-bash
容器中创建一个新的Bash会话。