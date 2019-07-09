# PPTP for Ubuntu

{{indexmenu_n>21}}

**安装PPP，PPTP**

    # apt-get install pptpd

**编辑pptp.conf，在最后加入以下两行代码**

    # vim /etc/pptpd.conf

    localip 10.8.0.1
    remoteip 10.8.0.10-100

**编辑options.pptpd，在最后加入以下两行代码**

    # vim /etc/ppp/pptpd-options

    ms-dns 8.8.8.8
    ms-dns 8.8.4.4

**编辑chap-secrets，account为pptp登录帐号，password为登录密码，其他默认**

    # vim /etc/ppp/chap-secrets

    # client        server      secret            IP addresses
      account       pptpd       password          *

**编辑sysctl.conf，开启网络转发功能**

    # vim /etc/sysctl.conf

    net.ipv4.ip_forward = 1

    # sysctl -p

**配置NAT**

``` 
# iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE 
```

**这边需要注意的是Debian/Ubuntu上iptables是不会保存规则的。**  
需要按如下步骤进行配置，让网卡关闭时保存iptables规则，启动时加载iptables规则：

创建/etc/network/if-post-down.d/iptables 文件

    # vim /etc/network/if-post-down.d/iptables

添加如下内容：

    #!/bin/bash
    iptables-save > /etc/iptables.rules

保存并退出，然后添加执行权限。

    # chmod +x /etc/network/if-post-down.d/iptables

创建/etc/network/if-pre-up.d/iptables 文件

    # vim /etc/network/if-pre-up.d/iptables

添加如下内容：

    #!/bin/bash
    iptables-restore < /etc/iptables.rules

保存并退出，然后添加执行权限。

    # chmod +x /etc/network/if-pre-up.d/iptables

**启动PPTP服务**

    # service pptpd start

或者

    # /etc/init.d/pptpd start

**设置为开机启动**

    # vim /etc/rc.local

将“ **/etc/init.d/pptpd start** ”加入到“/etc/rc.local”文件中  
保存并退出

**开通防火墙端口**

在后台，“防火墙管理”，选中您主机应用的防火墙，点击编辑。

![image](/images/pptp_firewall.01.png)

点击“添加规则”，填写如红色框中所示，“应用规则”。

![image](/images/pptp_firewall.02.png)
