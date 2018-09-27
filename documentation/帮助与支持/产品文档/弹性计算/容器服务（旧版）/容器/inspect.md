# **inspect**

Usage:jcloud inspect [OPTIONS] CONTAINER|IMAGE [CONTAINER|IMAGE...]
Return low-level information on a container or image
-f, --format Format the output using the given go template
--help Print usage
-s, --size Display total file sizes if the type is container
--type Return JSON for specified type, (e.g image or container)

默认情况下，该命令将以JSON数组的形式返回所有结果。如果容器和镜像名称相同，则将返回未指定类型的容器JSON数据。如果指定格式，则结果将按给定格式显示。

GO语言的

text/template
包描述了格式的所有细节。

示例

**获取实例的IP地址：**

大多数情况下，你可以直接选择JSON数据的任何字段。
$ jcloud inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $INSTANCE_ID

**获取实例的MAC地址：**

大多数情况下，你可以直接选择JSON数据的任何字段。
$ jcloud inspect --format='{{range .NetworkSettings.Networks}}{{.MacAddress}}{{end}}' $INSTANCE_ID

**获取实例的日志路径：**

$ jcloud inspect --format='{{.LogPath}}' $INSTANCE_ID

**列出所有端口的绑定情况：**

对结果进行循环排列和映射以产生简单的文本输出：
$ jcloud inspect --format='{{range $p, $conf := .NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' $INSTANCE_ID

**查找指定端口的映射：**

当字段名称以数字为开头时，

.Field
语法是行不通的，但是模板语言中的index函数是可以的。

.NetworkSettings.Ports
部分包含内部端口映射到外部地址/端口对象列表的映射。要获取数字公共端口，可以使用

index
去查找指定端口映射，

index

0
包含其第一个对象。然后可以访问

HostPort
字段获取公共地址。
$ jcloud inspect --format='{{(index (index .NetworkSettings.Ports "8787/tcp") 0).HostPort}}' $INSTANCE_ID

**获取JSON格式的子部分：**

如果你请求的一个字段其本身包含其他字段，默认情况下你会得到一个Go-style内部值的转储。 Jcloud添加了一个模板函数

json
，它用于获取JSON格式的结果。
$ jcloud inspect --format='{{json .Config}}' $INSTANCE_ID