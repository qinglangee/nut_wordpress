# linux 网卡参数配置

## IP 网关 相关的配置

*centos 配置*  `vim /etc/sysconfig/network-scripts/ifcfg-eth0`
ifcfg-eth0  (centos7 装好后，会生成ifcfg-em1, ifcfg-em2之类的文件，应该就是默认名字变了)

	TYPE=Ethernet
	#BOOTPROTO=dhcp
	BOOTPROTO=static  # 域名设置为静态的, 不使用dhcp 动态分配
	DEFROUTE=yes
	PEERDNS=yes
	PEERROUTES=yes
	IPV4_FAILURE_FATAL=no
	IPV6INIT=yes
	IPV6_AUTOCONF=yes
	IPV6_DEFROUTE=yes
	IPV6_PEERDNS=yes
	IPV6_PEERROUTES=yes
	IPV6_FAILURE_FATAL=no
	NAME=enp2s0
	UUID=297e6aaa-0ff4-4ccd-a95a-4178bbd37911
	DEVICE=enp2s0
	ONBOOT=yes

	GATEWAY=192.168.1.1   #添加网关
	NETMASK=255.255.255.0 #掩码
	IPADDR=192.168.1.102  #添加IP地址
	DNS1=192.168.0.1
*ubuntu 配置*

	vim /etc/network/interfaces

	auto lo
	iface lo inet loopback

	auto eth0
	#iface eth0 inet dhcp    # 这个是DHCP动态分配IP
	iface eth0 inet static
	address 192.168.50.124
	netmask 255.255.255.0
	gateway 192.168.50.1