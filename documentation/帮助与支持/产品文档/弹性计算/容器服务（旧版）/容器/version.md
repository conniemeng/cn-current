# **version**

Usage: jcloud version [OPTIONS]
Show the Jcloud.com CLI version information.
-f, --format="" Format the output using the given go template
--help=false Print usage

默认情况下，此命令会将所有的版本信息通过简单易读的方式展示出来。如果格式已经被指定，将按指定格式输出。

Go语言的[text/template](http://golang.org/pkg/text/template/)包描述了模板的所有细节。

## 示例

**默认输出：**

$ jcloud version
Client:
Version: 2016-01-12
Go version: go1.4.2
Git commit: f5bae0a
Built: DEC 23 17:56:00 UTC 2015
OS/Arch: linux/amd64
Cloud:
Endpoint: https://cs-cn-north-2.jcloud.com/
API version: 2015-12-16
Default Region: US/New York (us-ny)