VPN 架设中一些问题的解决方法（pptpd）
最近尝试了下VPN的架设，期间遇到的一些问题在此做个记录和总结：

1.pptpd已启动运行，但不能正常连接，查看messages发现以下记录：

 

MGR: connections limit (100) reached, extra IP addresses ignored

MGR: Manager process started

MGR: Maximum of 100 connections available

   通过搜索，查得解决方法如下：

   a.打开配置文件/etc/pptpd.conf，注释掉其中的logwtmp，如下所示：

 

    # TAG: logwtmp

    #       Use wtmp(5) to record client connections and disconnections.

    #

    #logwtmp

   b.确保在iptables打开了1723端口：

       -A INPUT -p tcp -m state --state NEW -m tcp --dport 1723 -j ACCEPT

   通过以上几步应该可以解决问题。

 

2.VPN可以连接成功，但不能正常上网，messages中记录如下：

       Cannot determine ethernet address for proxy ARP

   该问题主要出在没有相关的转发规则。需要进行如下配置：

   a.打开配置文件/etc/sysctl.conf，修改配置项net.ipv4.ip_forward为1：    

    # Controls IP packet forwarding

    net.ipv4.ip_forward = 1

       该配置项用于允许ip转发。

   b.还需在iptables中加入NAT转换：

       iptables -t nat -A POSTROUTING -s 192.168.0.0/255.255.255.0 -j SNAT --to-source 192.168.0.88

       其中192.168.0.0/255.255.255.0为VPN的内部网络，192.168.0.88当然就是服务器的地址了。
