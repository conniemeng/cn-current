# **Floating IP**

Floating IP或FIP，是一个公网可达的IP地址，您可以将FIP绑定到容器上。

同一地域下未绑定的公网IP可以被绑定到任何容器上。**您可以使用[jcloud fip allocat](https://www.jcloud.com/help/detail/645/isCateLog/1)申请一个公网IP：**
$ jcloud fip allocate 1
Please note that Floating IP (FIP) is billed monthly ($1). The billing begins when a new IP is allocated, ends when it is released. Partial month is treated as a entire month. Do you want to continue? [y/n]: y
52.68.129.19

**使用[jcloud fip attach](https://www.jcloud.com/help/detail/646/isCateLog/1)将公网IP绑定到指定容器上：**

$ jcloud fip attach 52.68.129.19 myweb
myweb

**使用[jcloud fip detach](https://www.jcloud.com/help/detail/647/isCateLog/1)将公网IP从指定容器上解绑：**

$ jcloud fip detach web
52.68.129.19

一个Fip只能绑定到一个容器。如果您需要将一个已绑定的Fip绑定到另一个容器，您需要先执行解绑操作，再执行绑定操作：

$ jcloud fip detach myweb && jcloud fip attach 52.68.129.19 myweb2

**使用[jcloud fip release](https://www.jcloud.com/help/detail/649/isCateLog/1)删除FIP**删除容器时，FIP会自动被解绑。如果您不再需要FIP，可以手动释放FIP：

$ jcloud fip release 52.68.129.19
52.68.129.19

**停止和重启容器**
容器执行停止或重启后，FIP不会被解绑：

$ jcloud stop myweb
myweb
$ jcloud ps -a
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
3259d441edae ghost "/entrypoint.sh npm s" 16 minutes ago Exited (0) 4 seconds ago myweb 23.236.114.91
$ jcloud start myweb
myweb
$ jcloud ps -a
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES PUBLIC IP
3259d441edae ghost "/entrypoint.sh npm s" 17 minutes ago Up 4 seconds 0.0.0.0:2368->2368/tcp myweb 23.236.114.91