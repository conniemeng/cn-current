# **kill**

Usage: jcloud kill [OPTIONS] CONTAINER
Kill a running container
--help Print usage

容器内的主进程将会收到

SIGKILL命令

。

注意：

ENTRYPOINT
和

CMD作为

/bin/sh -c
的子命令运行，将不会接收SIGKILL命令。也就是说不传递信号的子命令来运行。这意味着，可执行命令并非容器的PID 1进程，不会接收Unix指令。