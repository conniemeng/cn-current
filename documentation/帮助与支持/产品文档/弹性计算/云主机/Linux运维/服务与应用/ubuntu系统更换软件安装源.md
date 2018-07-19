## ubuntu系统更换软件安装源

使用官方镜像的Ubuntu云主机默认使用京东云内部软件安装源，如需更换为国内清华源，请按照以下步骤操作：

1、备份原有源文件：cp /etc/apt/sources.list /etc/apt/sources.list.backup
2、vi /etc/apt/sources.list

编辑源文件，将内容替换为需要更换的源，使用清华源可参考清华源官网（https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/）编辑源文件，编辑后保存。

3、apt-get update使源文件生效，安装软件验证是否正常

注意如果源文件的条目使用https链接，在执行apt-get update时有可能会卡在working[0%]无法继续。此时需要将源文件中每条下载链接的https修改为http，如图所示：![捕获.JPG](http://img1.jcloudcs.com/cms/8976f52b-5a65-4149-a371-3c3c3ddd0d1920180303105354.JPG)

将所有https修改为http![image.png](http://img1.jcloudcs.com/cms/8361f262-3dcf-4056-98dd-73c26732d40020180303105511.png)

修改完毕后保存文件再次尝试更新源。

如需更换回京东云内部源，执行cp /etc/apt/sources.list.backup /etc/apt/sources.list将源文件替换回原有备份文件后执行apt-get upadate即可。