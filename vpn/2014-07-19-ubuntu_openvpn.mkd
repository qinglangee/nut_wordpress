# ubuntu上安装openvpn

## 下载和配置

	sudo apt-get install openvpn
修改server.conf, 生成keys和centos安装一样.

*ubuntu的配置iptables不太一样*  
配置文件保存后，现在开始配置网络相关设置，先开启转发功能

	echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf

使设定生效

	sysctl -p

开始配置防火墙了,先清空防火墙现有的设置，遇到错误，不用管它，进行下一个操作。

	iptables -t nat -F
	iptables -t nat -X
	iptables -t nat -P PREROUTING ACCEPT
	iptables -t nat -P POSTROUTING ACCEPT
	iptables -t nat -P OUTPUT ACCEPT
	iptables -t mangle -F
	iptables -t mangle -X
	iptables -t mangle -P PREROUTING ACCEPT
	iptables -t mangle -P INPUT ACCEPT
	iptables -t mangle -P FORWARD ACCEPT
	iptables -t mangle -P OUTPUT ACCEPT
	iptables -t mangle -P POSTROUTING ACCEPT
	iptables -F
	iptables -X
	iptables -P FORWARD ACCEPT
	iptables -P INPUT ACCEPT
	iptables -P OUTPUT ACCEPT
	iptables -t raw -F
	iptables -t raw -X
	iptables -t raw -P PREROUTING ACCEPT
	iptables -t raw -P OUTPUT ACCEPT

设置防火墙，允许nat，端口转发和常用的服务,需要注意的是第一行的-o venet0 在openvz下面是venet0,在xen下面可能是eth0，这是网卡的编号，大家可以用ifconfig查看，看第一块网卡是eth0还是 venet0，不要搞错了，搞错了就访问不了外面的互联网。

	iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

	iptables -A INPUT -i lo -j ACCEPT
	iptables -A INPUT -i ! lo -d 127.0.0.0/8 -j REJECT

	iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
	iptables -A OUTPUT -j ACCEPT

	iptables -A INPUT -p tcp --dport 80 -j ACCEPT
	iptables -A INPUT -p tcp --dport 3306 -j ACCEPT
	iptables -A INPUT -p tcp -m state --state NEW --dport 22 -j ACCEPT

	iptables -A INPUT -p udp --dport 1194 -j ACCEPT
	iptables -A INPUT -s 10.8.0.0/24 -p all -j ACCEPT
	iptables -A FORWARD -d 10.8.0.0/24 -j ACCEPT

	iptables -A INPUT -i tun+ -j ACCEPT
	iptables -A FORWARD -i tun+ -j ACCEPT

	iptables -A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT
	iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

	iptables -A INPUT -j REJECT
	iptables -A FORWARD -j REJECT

保存 防火墙规则，让它在下次启动系统时自动生效

	iptables-save > /etc/iptables.up.rules

新建网络启动时加载的脚本 vim /etc/network/if-pre-up.d/iptables
输入下面的内容

	#!/bin/bash
	/sbin/iptables-restore < /etc/iptables.up.rules

改变执行权限

	chmod a+x /etc/network/if-pre-up.d/iptables

等下次你启动系统的时候，防火墙就会以现在的规则执行。
现在既然配置都己经好了，那就重启openvpn服务吧

	/etc/init.d/openvpn restart

## 客户端配置


refs:  
[Configure OpenVPN on Ubuntu][1]  
[openvz vps ubuntu 安装 openvpn 并配置iptables防火墙][2]  
[UBUNTU 安装OPENVPN ][3]  
[How to install OpenVPN on a Debian/Ubuntu VPS instantly][4]


[1]: http://forum.ubuntu.com.cn/viewtopic.php?p=532825
[2]: http://iam.ittot.com/read.php/1120.htm
[3]: http://blog.csdn.net/tianxiajianling/article/details/7767119
[4]: http://vpsnoc.com/blog/2010/01/how-to-install-openvpn-on-a-debianubuntu-vps-instantly/