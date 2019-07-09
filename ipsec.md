# IPSec VPN

{{indexmenu_n>30}}

## 1、安装 openswan 及其环境

1.1、软件安装

CentOS:

    yum install -y openswan lsof

Ubuntu:

    apt-get update
    apt-get install -y openswan lsof

Ubuntu 会交互安装，第一个询问启用 X.509 证书的时候选择 no，第二个只要点 ok 就可以。

1.2、开启 linux 主机的路由功能（所有为ipsec vpn server 的主机都要开启）

修改 /etc/sysctl.conf文件：

    Controls IP packet forwarding net.ipv4.ip_forward = 1

（开启主机路由转发）

    Controls source route verification net.ipv4.conf.default.rp_filter = 0

（关闭源路由验证）

修改 /etc/sysctl.conf文件，加入以下内容:

    net.ipv4.ip_forward = 1
    net.ipv4.conf.default.rp_filter = 0

修改完成后执行 sysctl -p 加载配置。

1.3、在控制台上的防火墙添加 ipsec vpn 所用的端口

![image](/images/vpn01.jpg)

![image](/images/vpn02.jpg)

## 2、配置服务

2.1 检测服务正常（所有为 ipsec vpn server 的主机）

service ipsec start

![image](/images/vpn03.jpg)

ipsec verify（一个 N/A 和一个 DISABLED 不影响 ipsec vpn 的建立，Ubuntu 主机可能在checking
/bin/sh 会多一个 warning，也不影响。）

![image](/images/vpn04.jpg)

2.2 配置认证 key（所有为 ipsec vpn server 的主机）

vim /etc/ipsec.secrets

    #include /etc/ipsec.d/*.secrets
    
    #源IP 目标IP: PSK "(key)" （0.0.0.0 即为所有 vpn 都使用这个 key）
    
    0.0.0.0   0.0.0.0 : PSK "Ucloud.cn"  （注意空格格式不能错）

2.3 配置VPN主体

2.3.1 跨外网云主机间（云主机和其他公司内网 linux 主机）互通

![image](/images/vpn05.jpg)

![image](/images/vpn06.jpg)

2.3.2 云主机和外网 linux 主机间互通

![image](/images/vpn07.jpg)

![image](/images/vpn08.jpg)

2.3.3 云主机和其他网络设备之间的互通

![image](/images/vpn09.jpg)

![image](/images/vpn10.jpg)

对端网络设备（B）配置参数：

Peer 的 ip 为云主机的外网 ip 即 A.A.A.A

第一阶段选择 ikev1 主模式（main mode），参数为 3des、sha、group2。

第二阶段选择模式为 tunnel，参数为 esp、3des、sha。

启用 pfs 和 nat-t（nat 穿越）。

感兴趣流为 b.b.0.0/16 到 a.a.0.0/16，即用户端网段到云主机网段。

## 3、测试完成与错误定位

3.1 测试

```
ipsec auto --up net-to-net
```

![image](/images/vpn11.jpg)

```
service ipsec status
```

![image](/images/vpn12.jpg)

这个状态即为启动成功，两端可互相 ping 通。

3.2 VPN自动启动

    chkconfig ipsec on

![image](/images/vpn13.jpg)

将/etc/ipsec.conf 文件中的 auto=add 改为 auto=start

3.3 其他主机路由

其他云主机如果要通过 ipsec 访问对端要增加相应的路由，或者网关指向本地的 ipsec服务器。

3.4 故障排查 发生no connection named
“xxxxx”的报错时基本为配置文件错误或者conn名字错误，检查conn名称、配置文件格式，并查看/var/log/messages中具体错误参数/格式提示。

![image](/images/vpn14.jpg)

发生第一阶段（STATE\_MAIN\_I1）或者第二阶段（STATE\_QUICK\_I1）初始化超时报错的时候，多为两端参数配置错误导致的协商失败，需要查看/var/log/secure以及对端的日志确定具体哪个参数协商错误。

![image](/images/vpn15.jpg)
