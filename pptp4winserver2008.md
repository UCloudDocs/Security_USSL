# PPTP for Windows Server 2008

{{indexmenu_n>23}}

1.点击“开始”右侧的“服务器管理”图标

2.选择“角色”，在右侧“角色摘要”中，点击“添加角色”

![image](/images/pptp_win2008.02.png)

3.点击“下一步”

![image](/images/pptp_win2008.03.png)

4.选择“网络策略和访问服务”，点击“下一步”。

![image](/images/pptp_win2008.04.png)

5.选择“远程访问服务”和“路由”，点击“下一步”。

![image](/images/pptp_win2008.05.png)

6.点击“安装”。

![image](/images/pptp_win2008.06.png)

7.点击“关闭”。

![image](/images/pptp_win2008.07.png)

8.角色 --\> 右击“路由和远程访问” --\> 点击“配置并启用路由和远程访问”。

![image](/images/pptp_win2008.08.png)

9.点击“下一步”。

![image](/images/pptp_win2008.09.png)

10.选择“自定义配置”，点击“下一步”。

![image](/images/pptp_win2008.10.png)

11.选择“VPN访问”和“NAT”选项，点击“下一步”。

![image](/images/pptp_win2008.11.png)

12.点击“完成”。

![image](/images/pptp_win2008.12.png)

13.点击“确定”。

![image](/images/pptp_win2008.13.png)

14.点击“启动服务”。

![image](/images/pptp_win2008.14.png)

15.在如图路径，右击“NAT”，点击“新增接口”。

![image](/images/pptp_win2008.15.png)

16.选择“eth0”，点击“确定”。

![image](/images/pptp_win2008.16.png)

17.选择“公网接口连接到 Internet”，并且选择“在此接口上启用NAT”，点击“应用”。

![image](/images/pptp_win2008.17.png)

18.切换到“服务和端口”选项卡，选择“VPN网关（PPTP）”。

![image](/images/pptp_win2008.18.png)

19.在跳出的窗口中输入本机内网IP地址，点击“确定”。

![image](/images/pptp_win2008.19.png)

20.右击“路由和远程访问”，点击“属性”。

![image](/images/pptp_win2008.20.png)

21.切换到“IPv4”选项卡，选择“静态地址池”，点击“添加”。

![image](/images/pptp_win2008.21.png)

22.输入VPN连接到此服务器所要分配的IP地址段，点击“确定”。

![image](/images/pptp_win2008.22.png)

23.“配置” --\> “本地用户和组” --\> “用户”，右击“Administrator”，选择“属性”。  
（当然，您也可以建立一个组，或者配合AD来管理可VPN连接到此服务器的用户）

![image](/images/pptp_win2008.23.png)

24.切换到“拨入”选项卡，选择“允许访问”，点击“确认”。

![image](/images/pptp_win2008.24.png)

25.在后台，“防火墙管理”，选中您主机应用的防火墙，点击编辑。

![image](/images/pptp_win2008.25.1.png)

点击“添加规则”，填写如1723这条，“应用规则”。

![image](/images/pptp_win2008.25.2.png)
