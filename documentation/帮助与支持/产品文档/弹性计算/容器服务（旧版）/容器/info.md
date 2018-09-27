# **info**

Usage:jcloud info [OPTIONS]
Display system-wide information
--help Print usage

输出系统信息。

示例:
$ jcloud -D info
Containers: 14
Running: 3
Paused: 1
Stopped: 10
Images: 52
Server Version: 1.9.0
Storage Driver: aufs
Root Dir: /var/lib/jcloud/fontng Filesystem: extfs
Dirs: 545
Dirperm1 Supported: true
Execution Driver: native-0.2
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
Volume: local
Network: bridge null host
Kernel Version: 3.19.0-22-generic
OSType: linux
Architecture: x86_64
Operating System: Ubuntu 15.04
CPUs: 24
Total Memory: 62.86 GiB
Name: jcloud
ID: I54V:OLXT:HVMM:TPKO:JPHQ:CQCD:JNLC:O3BZ:4ZVJ:43XJ:PFHZ:6N2S
jcloud Root Dir: /var/lib/jcloud
Debug mode (client): true
Debug mode (server): true
File Descriptors: 59
Goroutines: 159
System Time: 2015-09-23T14:04:20.699842089+08:00
EventsListeners: 0
Init SHA1:
Init Path: /usr/bin/jcloud
jcloud Root Dir: /var/lib/jcloud
Http Proxy: //test:test@localhost:8080
Https Proxy: https://test:test@localhost:8080
WARNING: No swap limit support
Username: svendowideit
Registry: [https://index.docker.io/v1/]
Labels:
storage=ssd

-D为全局参数，打印所有容器的
调试信息。

如容器异常，请在命令行执行jcloud version、jcloud -D info命令，提交工单并上传命令执行结果的截图，以便我们快速定位问题。