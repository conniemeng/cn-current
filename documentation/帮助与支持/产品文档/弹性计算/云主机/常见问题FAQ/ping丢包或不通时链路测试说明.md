**ping丢包或不通时链路测试说明**

当客户端访问目标服务器出现 ping 丢包或 ping 不通时，可以通过mtr工具进行链路测试来判断问题来源。本文先介绍了进行链路测试的相关工具，然后对测试结果分析及测试步骤进行了说明。

**Linux 环境下链路测试工具介绍**

mtr （My traceroute）也是几乎所有 Linux 发行版本预装的网络测试工具。他把 ping和 traceroute 的功能并入了同一个工具中，所以功能更强大。mtr 默认发送 ICMP 数据包进行链路探测。可以通过 -u 参数来指定使用 UDP 数据包用于探测。相对于 traceroute 只会做一次链路跟踪测试，mtr 会对链路上的相关节点做持续探测并给出相应的统计信息。所以，mtr能避免节点波动对测试结果的影响，所以其测试结果更正确，建议优先使用。

用法说明：

mtr [-hvrctglspni46] [—help] [—version] [—report] [—report-cycles=COUNT] [—curses] [—gtk] [—raw] [—split] [—no-dns] [—address interface] [—psize=bytes/-s bytes] [—interval=SECONDS] HOSTNAME [PACKETSIZE]

示例输出：

[root@liuxw-test ~]/# mtr 125.94.39.249 My traceroute [v0.75]liuxw-test.jcloud.local (0.0.0.0) Wed Aug 30 10:23:38 2017Resolver error: Answered class does not match queried class.ields quit Packets Pings Host Loss% Snt Last Avg Best Wrst StDev 1. 10.254.2.254 0.0% 32 0.8 0.8 0.6 1.2 0.1 2. 100.127.228.13 0.0% 32 1.1 1.2 1.0 1.6 0.2 3. ??? 4. 105.96.135.219.broad.fs.gd.dynam 0.0% 32 3.9 4.0 2.0 6.4 1.6 5. 113.108.208.209 0.0% 32 8.4 6.7 4.8 8.9 1.4 6. 202.97.65.101 0.0% 32 42.5 42.5 40.8 44.8 1.2 7. 220.181.0.198 74.2% 32 37.6 37.7 37.6 37.7 0.0 8. 220.181.0.106 74.2% 32 40.2 40.2 40.2 40.3 0.1 9. 218.30.28.161 96.8% 32 40.4 40.4 40.4 40.4 0.010. 180.149.140.34 15.6% 32 40.1 40.2 39.7 47.0 1.411. 101.200.109.129 0.0% 32 42.0 41.7 40.7 43.5 0.612. 106.11.130.189 0.0% 32 40.9 41.1 40.6 44.2 0.813. ???14. 123.57.221.198 0.0% 31 44.7 40.7 40.4 44.7 0.8

常见可选参数说明：

-r 或 —report：以报告模式显示输出。

-p 或 —split：将每次追踪的结果分别列出来，而非如 —report统计整个结果。

-s 或 —psize：指定ping数据包的大小。

-n 或 —no-dns：不对IP地址做域名反解析。

-a 或 —address：设置发送数据包的IP地址。用于主机有多个IP时。

-4：只使用 IPv4 协议。

-6：只使用 IPv6 协议。

另外，也可以在 mtr 运行过程中，输入相应字母来快速切换模式，比如：

？或 h：显示帮助菜单。

d：切换显示模式。

n：切换启用或禁用 DNS 域名解析。

u：切换使用 ICMP或 UDP 数据包进行探测。

返回结果说明：

默认配置下，返回结果中各数据列的说明：

第一列（Host）：节点IP地址和域名。如前面所示，按n键可以切换显示。

第二列（Loss%）：节点丢包率。

第三列（Snt）：每秒发送数据包数。默认值是10，可以通过参数 -c 指定。

第四列（Last）：最近一次的探测延迟值。

第五、六、七列（Avg、Best、Wrst）：分别是探测延迟的平均值、最小值和最大值。

第八列（StDev）：标准偏差。越大说明相应节点越不稳定。

**Windows环境下链路测试工具介绍**

WinMTR 是 mtr 工具在 Windows 环境下的图形化实现，但进行了功能简化，只支持 mtr部分参数的调整设置。WinMTR 默认发送ICMP 数据包进行探测，无法切换。WinMTR 可以从其[官方网站](http://winmtr.net/download-winmtr/?spm=5176.7740573.2.8.5uWrGK "官方网站")下载获取。和 mtr 一样，相比 tracert，WinMTR 能避免节点波动对测试结果的影响，所以测试结果更正确。所以，在 WinMTR 可用的情况下，建议优先使用 WinMTR 进行链路测试。

用法说明：

WinMTR 无需安装，直接解压运行即可。操作方法非常简单，说明如下：

1.如下图所示，运行程序后，在 Host 字段输入目标服务器域名或 IP（注意前面不要包含空格）。

![1.png](https://img1.jcloudcs.com/cms/42f62652-7517-4800-8151-925220f97b5920171013161859.png)

2.点击 Start 开始测试（开始测试后，相应按钮变成了 Stop）。

![2.png](https://img1.jcloudcs.com/cms/0aadb227-d515-4c4e-a384-277cbb0e887420171013161929.png)

3.运行一段时间后，点击 Stop 停止测试。

4.其它选项说明：

Copy Text to clipboard：将测试结果以文本格式复制到粘贴板。

Copy HTML to clipboard：将测试结果以 HTML 格式复制到粘贴板。

Export TEXT：将测试结果以文本格式导出到指定文件。

Export HTML：将测试结果以 HTML 格式导出到指定文件。

Options：可选参数，包括：

Interval（sec）：每次探测的间隔（过期）时间。默认为 1 秒。

Ping size(bytes)： ping 探测所使用的数据包大小，默认为 64 字节。

Max hosts in LRU list： LRU 列表支持的最大主机数，默认值为 128。

Resolve names：通过反查 IP 以域名显示相关节点。

返回结果说明：

默认配置下，返回结果中各数据列的说明：

第一列（Host）：节点IP地址和域名。如前面所示，按n键可以切换显示。

第二列（Loss%）：节点丢包率。

第三列（Snt）：每秒发送数据包数。默认值是10，可以通过参数 -c 指定。

第四列（Last）：最近一次的探测延迟值。

第五、六、七列（Avg、Best、Wrst）：分别是探测延迟的平均值、最小值和最大值。

第八列（StDev）：标准偏差。越大说明相应节点越不稳定。

如无法解决您的问题，请向我们提工单。