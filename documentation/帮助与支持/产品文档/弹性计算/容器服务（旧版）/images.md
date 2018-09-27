# **image****s**

Usage: jcloud images [OPTIONS] [REPOSITORY[:TAG]]
List images
-a, --all=false Show all images (default hides intermediate images)
--digests=false Show digests
-f, --filter=[] Filter output based on conditions provided
--help=false Print usage
--no-trunc=false Don't truncate output
-q, --quiet=false Only show numeric IDs

默认的

jcloud images
命令会列出所有的顶层镜像，包括他们的储存库和标签以及他们的虚拟大小。

Docker镜像具有中间层，可以通过允许缓存每个步骤来提高可重用性、降低磁盘使用率以及加速构建速度。默认情况下不显示这些中间层。

虚拟大小是指镜像及其所有父镜像占用的累计空间。也是

docker save
命令创建的Tar文件的内容所使用的磁盘空间。

如果一个镜像具有不同的tags或者被保存在多个镜像仓库中，那么该镜像会被多次列出。系统为具有相同ID的镜像分配一个固定大小的存储空间，空间大小为VIRTUAL SIZE列出的大小。

## **列出最近创建的镜像列表**

$ jcloud images
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
<none> <none> 77af4d6b9913 19 hours ago 1.089 GB
committ latest b6fa739cedf5 19 hours ago 1.089 GB
<none> <none> 78a85c484f71 19 hours ago 1.089 GB
docker latest 30557a29d5ab 20 hours ago 1.089 GB
<none> <none> 5ed6274db6ce 24 hours ago 1.089 GB
postgres 9 746b819f315e 4 days ago 213.4 MB
postgres 9.3 746b819f315e 4 days ago 213.4 MB
postgres 9.3.5 746b819f315e 4 days ago 213.4 MB
postgres latest 746b819f315e 4 days ago 213.4 MB

## **通过镜像****名****称和标签列出镜像**

jcloud images
命令使用一个可选参数

[REPOSITORY[:TAG]]
将镜像列表限制为与参数匹配的镜像。如果指定repository而不指定tag，

jcloud images
命令将会列出指定repository中的所有镜像。

例如，运行以下命令来列出“java”存储库中的所有镜像：
$ jcloud images java
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
java 8 308e519aac60 6 days ago 824.5 MB
java 7 493d82594c15 3 months ago 656.3 MB
java latest 2711b1d6f3aa 5 months ago 603.9 MB

参数

[REPOSITORY[:TAG]]
的值是“精确匹配”。这意味着，例如

jcloud images jav
命令匹配不到

java
镜像。

如果

REPOSITORY
和

TAG
都给定，只有与repository和tag都匹配的镜像才会被列出。你可以使用以下命令去列出所有repository是java并且tag为8的本地镜像：
$ jcloud images java:8
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
java 8 308e519aac60 6 days ago 824.5 MB

如果没有镜像匹配到参数

REPOSITORY[:TAG]
，列表返回为空。

$ jcloud images java:0
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE

## **完整列出镜像ID**

$ jcloud images --no-trunc
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
<none> <none> 77af4d6b9913e693e8d0b4b294fa62ade6054e6b2f1ffb617ac955dd63fb0182 19 hours ago 1.089 GB
committest latest b6fa739cedf5ea12a620a439402b6004d057da800f91c7524b5086a5e4749c9f 19 hours ago 1.089 GB
<none> <none> 78a85c484f71509adeaace20e72e941f6bdd2b25b4c75da8693efd9f61a37921 19 hours ago 1.089 GB
docker latest 30557a29d5abc51e5f1d5b472e79b7e296f595abcf19fe6b9199dbbc809c6ff4 20 hours ago 1.089 GB
<none> <none> 0124422dd9f9cf7ef15c0617cda3931ee68346455441d66ab8bdc5b05e9fdce5 20 hours ago 1.089 GB
<none> <none> 18ad6fad340262ac2a636efd98a6d1f0ea775ae3d45240d3418466495a19a81b 22 hours ago 1.082 GB
<none> <none> f9f1e26352f0a3ba6a0ff68167559f64f3e21ff7ada60366e2d44a04befd1d3a 23 hours ago 1.089 GB
tryout latest 2629d1fa0b81b222fca63371ca16cbf6a0772d07759ff80e8d1369b926940074 23 hours ago 131.5 MB
<none> <none> 5ed6274db6ceb2397844896966ea239290555e74ef307030ebb01ff91b1914df 24 hours ago 1.089 GB

## **列出镜像digests**

V2或更高版本的镜像拥有一个内容可寻址标识符，称为

digest
。只要用于生成镜像的输入不变，则镜像的digest值是可预测的。使用

--digests
可以列出镜像的digest值：
$ jcloud images --digests
REPOSITORY TAG DIGEST IMAGE ID CREATED VIRTUAL SIZE
localhost:5000/test/busybox <none> sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf 4986bf8c1536 9 weeks ago 2.43 MB

当向2.0版本的镜像仓库上传或下载镜像时，

push
和

pull
命令的输出包括镜像的digest值。你可以使用digest来下载镜像。你也可以参考create、run和rmi指令中的digest值以及Docker file中的FROM镜像引用。

## **Filter**

过滤标志（

-f
或

--filter

）
的格式为"key=value"。如果有多个过滤器，则传递多个标志位，例如，

--filter"foo=bar" --filter "bif=baz"
。

目前支持的过滤器有：

* 
dangling (布尔型 - true或false)
* 
label (

label=<key>
或

label=<key>=<value>
)

## **Untagged 镜像(dangling)**

$ jcloud images --filter "dangling=true"
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
<none> <none> 8abc22fbb042 4 weeks ago 0 B
<none> <none> 48e5f45168b9 4 weeks ago 2.489 MB
<none> <none> bf747efa0e2f 4 weeks ago 0 B
<none> <none> 980fe10e5736 12 weeks ago 101.4 MB
<none> <none> dea752e4e117 12 weeks ago 101.4 MB
<none> <none> 511136ea3c5a 8 months ago 0 B

该命令会显示未标记的镜像，即镜像树的子镜像节点（不是镜像的中间层）。如果在构建镜像时未指定repo:tag参数，新镜像仅包含镜像ID，那么镜像就会被标记为<none>:<none>或untagged。如果删除容器正在使用的镜像，系统会提示错误。使用dangling参数，可以对镜像进行批量删除。

$ jcloud rmi $(jcloud images -f "dangling=true" -q)
8abc22fbb042
48e5f45168b9
bf747efa0e2f
980fe10e5736
dea752e4e117
511136ea3c5a

注意：系统将会弹出警告，提示当前有使用untagged镜像创建的容器。

## **Labeled镜像**

label
过滤器基于标签本身或标签及其对应值来匹配镜像。

以下过滤器使用

com.example.version
标签对镜像进行匹配，未匹配标签值：
$ jcloud images --filter "label=com.example.version"
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
match-me-1 latest eeae25ada2aa About a minute ago 188.3 MB
match-me-2 latest eeae25ada2aa About a minute ago 188.3 MB

使用标签

com.example.version，
标签值等于1.0过滤器匹配镜像：

$ jcloud images --filter "label=com.example.version=1.0"
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
match-me latest eeae25ada2aa About a minute ago 188.3 MB

使用标签值为0.1的过滤器无法找到匹配的镜像，返回列表为空：

$ jcloud images --filter "label=com.example.version=0.1"
REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE