**登录Master节点**

介绍如何通过WEB界面登录和SSH登录集群Master节点。

* 
WEB界面登录

步骤1 根据Web提示信息，在浏览器中输入公网IP，即可查看到管理界面。

注意事项：参见创建集群-网络设置中登录Master节点第6.网络ACL

* 
SSH登录

步骤1根据SSH提示信息，通过SSH工具，用root用户远程登录Master节点。

![图片.png](https://img1.jcloudcs.com/cms/396d0810-b26c-4486-ba94-5acc5cf671a020180412160118.png)![图片.png](https://img1.jcloudcs.com/cms/a6b3d188-0ef0-4e2e-acbc-b589d1a36ae520180412160124.png)

步骤2 常用命令

1. 执行以下命令切换用户

[root@OmkZafrH-Master1 ~]/# sudo su - hadoop

2. 查看节点运行的服务进程

[hadoop@OmkZafrH-Master1 ~]$ jps

9344 RunJar

6675 ApplicationHistoryServer

5028 QuorumPeerMain

5190 DFSZKFailoverController

4840 JournalNode

7386 HMaster

4765 Bootstrap

19757 Jps

8685 JobHistoryServer

9550 ResourceManager

5455 NameNode

10287 RunJar

3. 查看软件安装位置及软件目录

软件位置默认放在根目录的data0文件下

[hadoop@OmkZafrH-Master1 ~]$ cd /data0/

[hadoop@OmkZafrH-Master1 data0]$ ll

total 56

drwxr-xr-x 9 hadoop hadoop 4096 Oct 31 18:07 apache-hive-2.1.1-bin

drwxr-xr-x 6 root root 4096 Apr 10 17:42 bdos

drwxr-xr-x 3 root root 4096 Apr 10 17:41 bfd

drwxr-xr-x 5 root root 4096 Apr 10 17:43 hadoop

drwxrwxrwx 11 hadoop hadoop 4096 Apr 10 17:42 hadoop-2.7.4

drwxr-xr-x 7 hadoop hadoop 4096 Oct 31 12:21 hbase-1.2.6

drwx------ 2 root root 16384 Apr 10 17:39 lost+found

drwxr-xr-x 4 root root 4096 Apr 10 17:41 var

drwxr-xr-x 3 root root 4096 Apr 10 17:43 yarn

drwxr-xr-x 3 hadoop hadoop 4096 Apr 10 17:42 zookeeper

drwxr-xr-x 10 hadoop hadoop 4096 Mar 23 2017 zookeeper-3.4.10

4. 查看环境变量

[hadoop@OmkZafrH-Master1 data0]$ vi ~/.bashrc

/# .bashrc

/# Source global definitions

if [ -f /etc/bashrc ]; then

. /etc/bashrc

fi

/# User specific aliases and functions

export HBASE_HOME=/data0/hbase-1.2.6

export PATH=$PATH:$HBASE_HOME/bin

export HBASE_HOME=/data0/hbase-1.2.6

export PATH=$PATH:$HBASE_HOME/bin

export HIVE_HOME=/data0/apache-hive-2.1.1-bin

export PATH=$PATH:$HIVE_HOME/bin

export HADOOP_HOME=/data0/hadoop-2.7.4

export PATH=$PATH:$HADOOP_HOME/bin

export HADOOP_LOG_DIR=/data0/var/log/hadoop

export HTTPFS_LOG=/data0/var/log/httpfs

export HADOOP_HOME=/data0/hadoop-2.7.4

export PATH=$PATH:$HADOOP_HOME/bin

export HADOOP_LOG_DIR=/data0/var/log/hadoop

export HTTPFS_LOG=/data0/var/log/httpfs

export ZOOKEEPER_HOME=/data0/zookeeper-3.4.10

export PATH=$PATH:$ZOOKEEPER_HOME/bin

export ZOO_LOG_DIR=/data0/var/log/zookeeper-3.4.10