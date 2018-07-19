**Windows2012安装.NET Framework 3.5.1报错找不到源文件**

**问题描述：**

使用 Windows Server 2012系统，在安装 .NET Framework 3.5.1 时报错，报错内容如下图所示：

![1.png](https://img1.jcloudcs.com/cms/9ddf03e4-76cd-4525-b8cc-bde66b24fd6c20170829150524.png)

**问题原因：**

找不到安装源文件。

**解决办法：**

1.从开始菜单中找到 PowerShell，右键单击选择 以管理员身份运行。

2.输入如下脚本后，按回车键执行。

1.Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0 2.Restart-Service -Name wuauserv 3.Install-WindowsFeature Net-Framework-Core 4.Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1 5.Restart-Service -Name wuauserv

如无法解决您的问题，请向我们提工单。