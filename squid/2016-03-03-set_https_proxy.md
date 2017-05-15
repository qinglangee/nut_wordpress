# squid 配置 https 代理服务器

最快的搭建方式为：[详细教程][1]

1. 执行yum install squid
2. 复制最下面的配置文件覆盖默认配置文件squid.conf
3. 生成密码文件（见下图）
4. 启动squid：service squid start

高匿检测工具页面    http://www.iprivacytools.com/proxy-checker-anonymity-test/ 

配置文件

	#################################
	###   acl和http_pass访问控制   ###
	#################################
	#acl manager proto cache_object
	acl localhost src 127.0.0.1/32 ::1
	acl to_localhost dst 127.0.0.0/8 0.0.0.0/32 ::1

	# 以下定义了局域网地址localnet（需要了解一些网络里面的私有地址概念）
	acl localnet src 10.0.0.0/8
	acl localnet src 172.16.0.0/12
	acl localnet src 192.168.0.0/16
	acl localnet src fc00::/7
	acl localnet src fe80::/10

	# 定义SSL_ports为443
	acl SSL_ports port 443

	# 定义了Safe_ports所代表的端口
	acl Safe_ports port 80      # http
	acl Safe_ports port 21      # ftp
	acl Safe_ports port 443     # https
	acl Safe_ports port 70      # gopher
	acl Safe_ports port 210     # wais
	acl Safe_ports port 1025-65535  # unregistered ports
	acl Safe_ports port 280     # http-mgmt
	acl Safe_ports port 488     # gss-http
	acl Safe_ports port 591     # filemaker
	acl Safe_ports port 777     # multiling http

	# 定义CONNECT代表http里的CONNECT请求方法
	acl CONNECT method CONNECT

	# 允许本机管理缓存
	http_access allow manager localhost
	# 拒绝其他地址管理缓存
	http_access deny manager

	# 拒绝不安全端口请求
	http_access deny !Safe_ports

	# 不允许连接非安全SSL_ports端口
	http_access deny CONNECT !SSL_ports

	# 拒绝连接到本地服务器提供的服务
	# （用于保护本机一些只有本机用户才能访问的服务）
	# http_access deny to_localhost

	# 允许局域网用户的请求
	http_access allow localnet
	# 允许本机用户的请求
	http_access allow localhost

	#http_access allow 106.2.200.98

	# 拒绝其他所有请求
	#http_access deny all
	http_access allow all

	#################################
	###   squid 服务器基本配置      ###
	#################################

	# Squid的监听端口
	# http_port 3128
	http_port 36666

	#################################
	###   squid 缓存配置           ###
	#################################

	# 出现cgi-bin或者？的URL不予缓存
	hierarchy_stoplist cgi-bin ?

	# 磁盘缓存目录
	#cache_dir ufs /var/spool/squid 100 16 256

	# squid挂掉后，临终遗言要放到哪里
	coredump_dir /var/spool/squid

	# 刷新缓存规则
	refresh_pattern ^ftp:       1440    20% 10080
	refresh_pattern ^gopher:    1440    0%  1440
	refresh_pattern -i (/cgi-bin/|\?) 0 0%  0
	refresh_pattern .       0   20% 4320
	# 设置高匿名代理
	#Squid 3.1
	via off
	forwarded_for delete




refs:  
[使用 Squid 搭建正向代理][1]  
[squid 设置高度匿名代理](http://ju.outofmemory.cn/entry/231842)  


[1]: http://www.williamsang.com/archives/1645.html