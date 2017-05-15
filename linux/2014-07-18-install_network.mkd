# 网卡驱动坏掉了
装 network-manager-openvpn时, 把网卡装坏了
## 安装驱动
查看网卡驱动的安装情况, 没有eth0一般就是驱动没装好

	ifconfig       # 显示启用的
	ifconfig -a    # 显示所有
查看驱动的型号

	lspci      # 看一下 net controller相关的信息
	lspci |grep "Ethernet controller"  # 这个一般就是网卡的信息
>$ lspci |grep "Ethernet controller"
>03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168 PCI Express Gigabit Ethernet controller (rev 06)


RTL8111/8168 就是型号, 上网查一下Realtek的牌子, 到官网下驱动,回来以后编译安装

	./configure && make && make install

安了后是好的, 安之前没看, 不知道之前是不是好的

## 配置网络信息 (IP 网关 DNS)

即时生效（重启后失效）:

	ifconfig eth0 192.168.1.102 netmask 255.255.255.0  //添加IP地址
	route add default gw 192.168.1.1   //添加网关
启动生效:
*centos 配置*

	vim /etc/sysconfig/network-scripts/ifcfg-eth0  

	GATEWAY=192.168.1.1 //添加网关
	NETMASK=255.255.255.0 //掩码
	IPADDR=192.168.1.102  //添加IP地址
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

手动设置DNS服务器：

	vim /etc/resolv.conf

	# 添加如下内容(这点所有Linux发行版都通用):

	nameserver 192.168.80.2
	nameserver 8.8.8.8

	# 重启网络服务
	/etc/init.d/networking restart  
>这样有个缺点，/etc/resolv.conf文件当每次重启时，系统会根据DHCP分配的信息重写这个文件，
>以前内容会被覆盖。因此这个方法治标不治本



refs:  
[Ubuntu 10.04 安装网卡驱动  ][1]  
[linux配置网卡IP地址命令详细介绍及一些常用网络配置命令][2]  
[linux下修改IP、DNS、路由命令行设置 ubuntu 版本命令行设置IP][3]  
[Ubuntu Server 12.04 静态IP简洁配置][4]  


[1]: http://blog.163.com/zhuandi_h/blog/static/180270288201211614856802/
[2]: http://www.2cto.com/os/201012/80325.html
[3]: http://www.cnblogs.com/fighter/archive/2010/03/04/1678007.html
[4]: http://www.ha97.com/4895.html