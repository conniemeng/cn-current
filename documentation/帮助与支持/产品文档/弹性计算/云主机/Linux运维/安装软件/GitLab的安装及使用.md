**GitLab的安装及使用**

**前言**

GitLab是利用 Ruby on Rails 一个开源的版本管理系统，实现一个自托管的Git项目仓库，可通过Web界面进行访问公开的或者私人项目。

它拥有与Github类似的功能，能够浏览源代码，管理缺陷和注释。可以管理团队对仓库的访问，它非常易于浏览提交过的版本并提供一个文件历史库。

团队成员可以利用内置的简单聊天程序(Wall)进行交流。

它还提供一个代码片段收集功能可以轻松实现代码复用，便于日后有需要的时候进行查找。

**Git的家族成员**

Git：是一种版本控制系统，是一个命令，是一种工具。

Gitlib：是用于实现Git功能的开发库。

Github：是一个基于Git实现的在线代码托管仓库，包含一个网站界面，向互联网开放。

GitLab：是一个基于Git实现的在线代码仓库托管软件，你可以用gitlab自己搭建一个类似于Github一样的系统，一般用于在企业、学校等内部网络搭建git私服。

**Gitlab的服务构成**

Nginx：静态web服务器。

gitlab-shell：用于处理Git命令和修改authorized keys列表。

gitlab-workhorse:轻量级的反向代理服务器。

logrotate：日志文件管理工具。

postgresql：数据库。

redis：缓存数据库。

sidekiq：用于在后台执行队列任务（异步执行）。

unicorn：An HTTP server for Rack applications，GitLab Rails应用是托管在这个服务器上面的。

**GitLab工作流程**

![1](http://cloudway.jcloud.com/wp-content/uploads/2017/05/1-1.png)

**GitLab Shell**

GitLab Shell有两个作用：为GitLab处理Git命令、修改authorized keys列表。

当通过SSH访问GitLab Server时，GitLab Shell会：

限制执行预定义好的Git命令（git push, git pull, git annex）

调用GitLab Rails API 检查权限

执行pre-receive钩子（在GitLab企业版中叫做Git钩子）

执行你请求的动作 处理GitLab的post-receive动作

处理自定义的post-receive动作

当通过http(s)访问GitLab Server时，工作流程取决于你是从Git仓库拉取(pull)代码还是向git仓库推送(push)代码。

如果你是从Git仓库拉取(pull)代码，GitLab Rails应用会全权负责处理用户鉴权和执行Git命令的工作；

如果你是向Git仓库推送(push)代码，GitLab Rails应用既不会进行用户鉴权也不会执行Git命令，它会把以下工作交由GitLab Shell进行处理：

1. 
调用GitLab Rails API 检查权限
1. 
执行pre-receive钩子（在GitLab企业版中叫做Git钩子）
1. 
执行你请求的动作
1. 
处理GitLab的post-receive动作
1. 
处理自定义的post-receive动作

**GitLab Workhorse**

GitLab Workhorse是一个敏捷的反向代理。它会处理一些大的HTTP请求，比如文件上传、文件下载、Git push/pull和Git包下载。其它请求会反向代理到GitLab Rails应用，即反向代理给后端的unicorn。

**Gitlab环境部署**

京东云配置要求：内存2G以上

进入镜像详情页面，单击立即购买，按提示步骤购买京东云实例。

购买完成之后，登录”京东云 管理控制台”,在左边导航栏里，单击”实例”，进入京东云实例列表页,选择所购京东云 实例所在的地域，并找到所购 京东云实例，在”IP 地址”列获取该实例的公网 IP 地址。

*注意：镜像部署好后默认是禁止远端访问的，所以直接访问京东云服务器的公网IP是不能访问到GitLab的登录界面的，请先运行/alidata目录下的gitlab_opennet.sh脚本，开启远程访问，然后再通过浏览器访问公网IP来访问GitLab的主页。*

方法二：手动部署：

1、配置yum源

1. 
vim /etc/yum.repos.d/gitlab-ce.repo

复制以下内容：

1. 
[gitlab-ce]
1. 
name=gitlab-ce
1. 
baseurl=http://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el6
1. 
Repo_gpgcheck=0
1. 
Enabled=1
1. 
Gpgkey=https://packages.gitlab.com/gpg.key

![2](http://cloudway.jcloud.com/wp-content/uploads/2017/05/2-2.png)

2、更新本地yum缓存

1. 
sudo yum makecache

![3](http://cloudway.jcloud.com/wp-content/uploads/2017/05/3-2.png)

3、安装GitLab社区版

1. 
curl -O https://downloads-packages.s3.amazonaws.com/centos-7.0.1406/gitlab-7.8.4_omnibus.1-1.el7.x86_64.rpm /#下载gitlab的rpm包
1. 
rpm -ivh gitlab-7.8.4_omnibus.1-1.el7.x86_64.rpm /#安装
1. 
![4](http://cloudway.jcloud.com/wp-content/uploads/2017/05/4-1.png)

GitLab常用命令：

1. 
sudo gitlab-ctl start /# 启动所有 gitlab 组件；
1. 
sudo gitlab-ctl stop /# 停止所有 gitlab 组件；
1. 
sudo gitlab-ctl restart /# 重启所有 gitlab 组件；
1. 
sudo gitlab-ctl status /# 查看服务状态；
1. 
sudo gitlab-ctl reconfigure /# 启动服务；
1. 
sudo vim /etc/gitlab/gitlab.rb /# 修改默认的配置文件；
1. 
gitlab-rake gitlab:check SANITIZE=true –trace /# 检查gitlab；
1. 
sudo gitlab-ctl tail /# 查看日志；

**GitLab使用**

**登录GitLab**

1、在浏览器的地址栏中输入京东云服务器的公网IP即可登录GitLab的界面，第一次登录使用的用户名和密码为 root 和 5iveL!fe。

![5](http://cloudway.jcloud.com/wp-content/uploads/2017/05/5-1.png)

2、首次登录会强制用户修改密码。密码修改成功后，输入新密码进行登录。

![6](http://cloudway.jcloud.com/wp-content/uploads/2017/05/6-1.png)

![7](http://cloudway.jcloud.com/wp-content/uploads/2017/05/7-1.png)

**创建Project**

1、安装Git工具linux：安装Git，使用自带的源安装。

1. 
yum install git

![8](http://cloudway.jcloud.com/wp-content/uploads/2017/05/8-1.png)

2、生成密钥文件

使用ssh-keygen生成密钥文件.ssh/id_rsa.pub。

![9](http://cloudway.jcloud.com/wp-content/uploads/2017/05/9-1.png)

![11](http://cloudway.jcloud.com/wp-content/uploads/2017/05/11.png)

3.在GitLab的主页中新建一个Project

![12](http://cloudway.jcloud.com/wp-content/uploads/2017/05/12-1.png)

![13](http://cloudway.jcloud.com/wp-content/uploads/2017/05/13-1.png)

4.添加ssh key导入步骤2中生成的密钥文件内容：

![14](http://cloudway.jcloud.com/wp-content/uploads/2017/05/14-1.png)

![15](http://cloudway.jcloud.com/wp-content/uploads/2017/05/15-1.png)

ssh key添加完成：

![16](http://cloudway.jcloud.com/wp-content/uploads/2017/05/16-1.png)

项目地址，该地址在进行clone操作时需要用到:

![17](http://cloudway.jcloud.com/wp-content/uploads/2017/05/17.png)

**简单配置**

1、配置使用Git仓库的人员姓名

1. 
git config –global user.name “京东云”

2、配置使用Git仓库的人员email，填写自己的公司邮箱

1. 
git config –global user.email “support@xxxx.com”

3、克隆项目，在本地生成同名目录，并且目录中会有所有的项目文件

1. 
git clone git@iZbp1h7fx16gkr9u4gk8v3Z:root/test.git

![18](http://cloudway.jcloud.com/wp-content/uploads/2017/05/18.png)

**上传文件**

1、进入到项目目录

1. 
cd test/

2、创建需要上传到GitLab中的目标文件

1. 
echo “test” > /root/test.sh

3、将目标文件或者目录拷贝到项目目录下

1. 
cp /root/test.sh ./

![19](http://cloudway.jcloud.com/wp-content/uploads/2017/05/19.png)

4、将test.sh文件加入到索引中

1. 
git add test.sh

5、将test.sh提交到本地仓库

1. 
git commit -m “test.sh”

6、将文件同步到GitLab服务器上

1. 
git push -u origin master

![20](http://cloudway.jcloud.com/wp-content/uploads/2017/05/20.png)

7、在网页中查看上传的test.sh文件已经同步到GitLab中

![](http://cloudway.jcloud.com/wp-content/uploads/2017/05/word-image-101.png)