# **stop**

Usage: jcloud stop [OPTIONS] CONTAINER
Stop a container
--help=false Print usage
-t, --time=10 Seconds to wait for stop before killing it

容器中的主进程将接收到

SIGTERM
，并在等待时间结束后执行

SIGKILL
。