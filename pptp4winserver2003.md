# PPTP for Windows Server 2003

{{indexmenu_n>22}}

1.“开始” -\> “设置” -\> “控制面板” -\> “管理工具” -\>
“路由和远程访问”；右击相应的服务器，选择“配置并启用路由和远程访问”。

![image](/images/pptp_win2003.01.png)

2.“下一步”

![image](/images/pptp_win2003.02.png)

3.选择“VPN访问”和“NAT和基本防火墙”。（如果只是需要连接VPN，不需要连上后上网，那么“NAT和基本防火墙”这个选择就不需要选择，步骤9也无需操作）

![image](/images/pptp_win2003.03.1.png)

![image](/images/pptp_win2003.03.2.png)

4.点击“完成”

![image](/images/pptp_win2003.04.png)

5.开启服务，点击“是”

![image](/images/pptp_win2003.05.png)

6.IP路由选择 --\> 右击“NAT和基本防火墙”--\>“新增接口”

![image](/images/pptp_win2003.06.png)

7.选择“eth0”，点击“确定”

![image](/images/pptp_win2003.07.png)

8.选择“公网接口连接到 Internet” --\> 选择“在此接口上启用NAT”，点击“应用”。

注：防火墙建议使用我们后台的防火墙，这边就不启用了。

![image](/images/pptp_win2003.08.png)

9.进入“服务和端口”选项卡，选择“VPN网关（PPTP）”和“远程桌面”。（如果您要提供http，pop等服务也需要在这里打开）

![image](/images/pptp_win2003.09.png)

10.在“专用地址”处填写本机的私有地址，点击“确定”。

![image](/images/pptp_win2003.10.png)

11.进入“ICMP”选项卡，选中“传入的回应请求”和“传入的时间戳请求”，点击“确定”。

![image](/images/pptp_win2003.11.png)

12.右击（本地）VPN服务器 --\> 属性 --\> “IP”选项卡 --\> 静态地址池 --\> 添加相应的VPN段内IP --\>
确定。

![image](/images/pptp_win2003.12.1.png)

![image](/images/pptp_win2003.12.2.png)

13.右击“我的电脑”--\>“管理” --\>
“用户”，进入如图所示的位置（当然，您也可以建立一个组，或者配合AD来管理可VPN连接到此服务器的用户）。在“Administrtaor”右击，点击“属性”。

![image](/images/pptp_win2003.13.png)

14.切换到“拨入”选项卡，选择“允许访问”，点击“应用”。

![image](/images/pptp_win2003.14.png)

15.在您的客户端设置正确的PPTP就行了，帐号为administrator，密码为administrator对应的密码。

16.在后台，“防火墙管理”，选中您主机应用的防火墙，点击编辑。

![image](/images/pptp_win2003.16.1.png)

点击“添加规则”，填写如1723这条，“应用规则”。

![image](/images/pptp_win2003.16.2.png)
