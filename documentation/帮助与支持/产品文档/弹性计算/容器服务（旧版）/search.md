# **search**

Usage: jcloud search [OPTIONS] TERM
Search the [Docker Hub](hub.docker.com) for images
--automated Only show automated builds
--help Print usage
--no-trunc Don't truncate output
-s, --stars Only displays with at least x stars

查询[Docker Hub](https://hub.docker.com/explore/)中的镜像

注意：查询语句最多返回25 个结果。

示例

## **通过名称查询镜像**

这个例子会列出名称中包含“busybox的”的镜像：

$ jcloud search busybox
NAME DESCRIPTION STARS OFFICIAL AUTOMATED
busybox Busybox base image. 316 [OK]
progrium/busybox 50 [OK]
radial/busyboxplus Full-chain, Internet enabled, busybox made... 8 [OK]
odise/busybox-python 2 [OK]
azukiapp/busybox This image is meant to be used as the base... 2 [OK]
ofayau/busybox-jvm Prepare busybox to install a 32 bits JVM. 1 [OK]
shingonoide/archlinux-busybox Arch Linux, a lightweight and flexible Lin... 1 [OK]
odise/busybox-curl 1 [OK]
ofayau/busybox-libc32 Busybox with 32 bits (and 64 bits) libs 1 [OK]
peelsky/zulu-openjdk-busybox 1 [OK]
skomma/busybox-data Docker image suitable for data volume cont... 1 [OK]
elektritter/busybox-teamspeak Leightweight teamspeak3 container based on... 1 [OK]
socketplane/busybox 1 [OK]
oveits/docker-nginx-busybox This is a tiny NginX docker image based on... 0 [OK]
ggtools/busybox-ubuntu Busybox ubuntu version with extra goodies 0 [OK]
nikfoundas/busybox-confd Minimal busybox based distribution of confd 0 [OK]
openshift/busybox-http-app 0 [OK]
jllopis/busybox 0 [OK]
swyckoff/busybox 0 [OK]
powellquiring/busybox 0 [OK]
williamyeh/busybox-sh Docker image for BusyBox's sh 0 [OK]
simplexsys/busybox-cli-powered Docker busybox images, with a few often us... 0 [OK]
fhisamoto/busybox-java Busybox java 0 [OK]
scottabernethy/busybox 0 [OK]
marclop/busybox-solr

## **通过名称或星数来查询镜像 （-s，--stars）**

此示例会显示镜像名称包含“busybox的” 并且至少有3 颗星的镜像：

$ jcloud search --stars=3 busybox
NAME DESCRIPTION STARS OFFICIAL AUTOMATED
busybox Busybox base image. 325 [OK]
progrium/busybox 50 [OK]
radial/busyboxplus Full-chain, Internet enabled, busybox made... 8 [OK]

## **查询自动生成镜像 （--automated）**

此示例会显示名称包含“busybox” ，至少有3 颗星而而是自动构建的镜像：

$ jcloud search --stars=3 --automated busybox
NAME DESCRIPTION STARS OFFICIAL AUTOMATED
progrium/busybox 50 [OK]
radial/busyboxplus Full-chain, Internet enabled, busybox made... 8 [OK]

## **显示完整描述（--no-TRUNC）**

此示例显示名称中包含“busybox” ，至少有3 颗星的镜像，并且输出不会被截断的镜像描述：

$ jcloud search --stars=3 --no-trunc busybox
NAME DESCRIPTION STARS OFFICIAL AUTOMATED
busybox Busybox base image. 325 [OK]
progrium/busybox 50 [OK]
radial/busyboxplus Full-chain, Internet enabled, busybox made from scratch. Comes in git and cURL flavors. 8 [OK]