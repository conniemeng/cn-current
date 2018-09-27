**Compose概述**

Compose 是一组定义和运行容器规则的命令集合。您可以编写一个Compose file来定义应用服务。 基于Compose文件，京东云实现了一键创建并启动服务的功能。

Compose 可以简单并快捷的部署和测试你的应用，其对于CI工作流也同样适用。你可以通过以下常见示例对Compose进行更深入的了解。

## **使用Compose 的基本步骤：**

* 
定义应用的 Docker 镜像并将其上传到 Docker hub 或者私有仓库，这样您就可以在任何地方复制您的应用。
* 
在docker-compose.yml 中定义组成应用的每一个服务，这样，这组服务就可以在一个隔离的环境单独运行。
* 
最后，运行[jcloud compose up](https://www.jcloud.com/help/detail/664/isCateLog/1) ，Compose将会启动并且运行你的整个应用。

与docker compose相比， jcloud compose 新增加了两个字段:

* 
size - 容器的大小，详情参考[容器概述](http://www.jcloud.com/help/detail/607/isCateLog/1)。
* 
fip - 为服务绑定的Floating IP。

## **示例：**

**申请一个FIP：**
$ jcloud fip allocate 1
Please note that Floating IP (FIP) is billed monthly ($1). The billing begins when a new IP is allocated, ends when it is released. Partial month is treated as a entire month. Do you want to continue? [y/n]: y
147.75.99.77

**docker-compose.yml文件示例如下（FIP请修改为您申请的IP地址）：**

version: '2'
services:
web:
image: wordpress:latest
fip: 147.75.99.77
links:
- db:mysql
depends_on:
- db
ports:
- "8080:80"
db:
image: mysql:latest
ports:
- "3306"
environment:
- MYSQL_ROOT_PASSWORD=my-secret-pw

**运行jcloud compose up，您可以在浏览器中访问您的wordpress（**http:///*/*/*./*/*/*./*/*/*./*/*/***）。**

更多详情，参考[Compose文件说明](https://www.jcloud.com/help/detail/662/isCateLog/1)。

## **Compose由一组指令组成，可以管理应用的整个生命周期：**

* 
启动、停止服务
* 
查看服务的运行状态
* 
使用日志流输出运行中容器的日志
* 
在服务上运行单次命令