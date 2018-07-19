**Windows系统远程桌面端口查看和修改方法**

********

**如何查看Windows远程桌面的端口：**

1.通过命令查看，点击 开始 - 运行 - 输入 cmd，确认 后打开命令窗口，执行如下命令：

tasklist /svc | find "Ter"

可以看到 TermService 的进程 ID 是 1764。

![1.png](https://img1.jcloudcs.com/cms/de79064d-a925-4d76-8cee-814006be700820170829171443.png)

再执行如下命令：

netstat -ano | find "1764"

即可看到服务所使用的端口，如下图所示是 3389

![2.png](https://img1.jcloudcs.com/cms/8a3c937f-9060-4f94-8861-277e904169a720170829172423.png)

2.打开注册表查看，在 运行 中输入 regedit 打开注册表编辑器。

![3.png](https://img1.jcloudcs.com/cms/c9fce89e-4b37-43e6-a2a9-a0d40e4d07f120170829173612.png)

查看HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp PortNumber 子键的值，如下图所示：

![5.png](https://img1.jcloudcs.com/cms/cca61caf-a604-4779-a2a4-932774ce025e20170829173642.png)

还需要查看 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp 下 portnumber 的值，两个值正常是相同的，就是远程服务的端口。

![4.png](https://img1.jcloudcs.com/cms/b7b050e2-63c2-4e7b-98e2-e1ad172dee7820170829173706.png)

**如何修改Windows远程桌面的端口：**

1.开始 - 运行 中输入 regedit 打开注册表编辑器。

2.依次展开 "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TerminalServer\Wds\rdpwd\Tds\tcp" 注册表项。其下的 PortNumber 键值所对应的端口号就是远程桌面端口，将其修改为用户需要的端口即可，如下图所示：

![6.png](https://img1.jcloudcs.com/cms/5b713934-a855-4124-8100-d3d0054cc8bf20170829181644.png)

3.再依次展开注册表中 "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TerminalServer\WinStations\RDP-Tcp" 注册表项。同样按照上面的方法将 PortNumber 键值进行更改保存，如下图所示：

![7.png](https://img1.jcloudcs.com/cms/3aabf128-6aad-409b-982a-a2482fb8bcb920170829181654.png)

注意：修改后需要检查防火墙、tcp/ip筛选中是否有安全规则限制，并需要重启服务器后生效。

如无法解决您的问题，请向我们提工单。