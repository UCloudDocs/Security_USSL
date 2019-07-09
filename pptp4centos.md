# PPTP for CentOS

{{indexmenu_n>20}}

**安装PPP，PPTP**

    # yum install -y ppp
    # rpm -ivh http://static.ucloud.cn/pptpd-1.3.4-2.el6.x86_64.rpm

注：32位请安装i686版本，将上面链接中的“x86\_64”改为“i686”即可，请根据自己的OS安装相应的版本。

**编辑pptp.conf，在最后加入以下两行代码**

    # vim /etc/pptpd.conf

    localip 10.8.0.1
    remoteip 10.8.0.10-100

**编辑options.pptpd，在最后加入以下两行代码**

    # vim /etc/ppp/options.pptpd

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

    # iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE 
    # iptables-save > /etc/sysconfig/iptables

**启动PPTP服务**

    # service pptpd start

**设置为开机启动**

    # chkconfig pptpd on
    # chkconfig iptables on

**开通防火墙端口**

在后台，“防火墙管理”，选中您主机应用的防火墙，点击编辑。

![image](/images/pptp_firewall.01.png)

点击“添加规则”，填写如红色框中所示，“应用规则”。

![image](/images/pptp_firewall.02.png)
