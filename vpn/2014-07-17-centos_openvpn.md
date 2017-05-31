# contos上安装 openvpn

## 下载和配置
Before we begin, you'll need to have the Extra Packages for Enterprise Linux (EPEL) Repository enabled on your cloud server. This is a third party repository offered by the Fedora Project which will provide the OpenVPN package
首先, 在服务器上要能访问到EPEL, 这是Fedora Project提供的第三方仓库, 上面有OpenVPN的安装包.

	wget http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
	rpm -Uvh epel-release-6-8.noarch.rpm
然后安装openvpn

	yum -y install openvpn
复制一个示例配置文件 

	cp /usr/share/doc/openvpn-*/sample-config-files/server.conf /etc/openvpn
	# 我的版本是这样的
	cp /usr/share/doc/openvpn-2.3.2/sample/sample-config-files/server.conf /etc/openvpn/
把push的注释去掉  (Our first change will be to uncomment the "push" parameter which causes traffic on our client systems to be routed through OpenVPN)

	push "redirect-gateway def1 bypass-dhcp"
修改DNS

	push "dhcp-option DNS 8.8.8.8"
	push "dhcp-option DNS 8.8.4.4"
为了安全起见, 让OpenVPN在启动后放弃权限. 把user和grout行的注释去掉

	user nobody
	group nobody

## 用easy-rsa产生密钥和证书
OpenVPN默认把需要的脚本放在文档目录,创建好需要的目录,把文件cp过去

	mkdir -p /etc/openvpn/easy-rsa/keys
	cp -rf /usr/share/openvpn/easy-rsa/2.0/* /etc/openvpn/easy-rsa
*奈何找不到easy-rsa的目录,自己下载个eash-rsa试试*
	
	git checkout v2.2.0
这样就有easy-rsa/2.0/* 了, 把文件cp到 /etc/openvpn/easy-rsa, 然后继续  
修改 `/etc/openvpn/easy-rsa/vars` 最后几行的默认内容, 
准备一个openssl的配置文件 

	cp /etc/openvpn/easy-rsa/openssl-1.0.0.cnf /etc/openvpn/easy-rsa/openssl.cnf
下面是创建各种签名文件

	cd /etc/openvpn/easy-rsa;source ./vars;./clean-all;./build-ca
	#  Now that we have our CA, we'll create our certificate for the OpenVPN server. When asked by build-key-server, answer yes to commit.

	./build-key-server server
	We're also going to need to generate our Diffie Hellman key exchange files using the build-dh script and copy all of our files into /etc/openvpn as follows:

	./build-dh
	cd /etc/openvpn/easy-rsa/keys
	cp dh1024.pem ca.crt server.crt server.key /etc/openvpn
创建客户端的文件

	./build-key client
打包留给客户端下载

	tar -cf /tmp/client.tar ca.crt client.crt client.key
## 路由配置 and 启动 OpenVPN 服务器
创建一条iptables规则来路由我们的VPN子网

	iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE
	service iptables save
然后, 在sysctl中 打开 IP Forwarding:

	vim /etc/sysctl.conf

	# Controls IP packet forwarding
	net.ipv4.ip_forward = 1
最后, 应用新的sysctl设置. 启动服务器并设置开机启动:

	sysctl -p
	service openvpn start
	chkconfig openvpn on
## 配置 OpenVPN 客户端
把服务器上的 ca.crt, client.crt, client.key 三个文件cp回客户端,然后创建一个 client.ovpn 文件, 内容如下(x.x.x.x换成vpn的ip):

	client
	dev tun
	proto udp
	remote x.x.x.x 1194
	resolv-retry infinite
	nobind
	persist-key
	persist-tun
	comp-lzo
	verb 3
	<ca>
	Contents of ca.crt
	</ca>
	<cert>
	Contents of client.crt
	</cert>
	<key>
	Contents of client.key
	</key>
linux 下连接 

	sudo openvpn --config ~/path/to/client.ovpn

## 其它注意事项
>请在使用openvpn之前，先设定本地机器上的dns为google或者opendns的dns服务器，这样方能正确的解析域名
>我们先检测下是否己经有开通tun和tap，检测是否开启tun功能的方法是：
>lsmod | grep tun
>如果没有显示, 再试试下面的命令
>modprobe tun
>这种检测手段并不很准确，为了保险起见 ，你还是联系下提供商，记住，一 定要开启TUN/TAP和iptables相关组件，不然配置会不成功。

# 下载使用easy-rsa

## git 地址

	git clone https://github.com/OpenVPN/easy-rsa.git

refs:  
[bridge的  Install OpenVPN to Configure Virtual Private Network.][1]  
[tun的  How to Setup and Configure an OpenVPN Server on CentOS 6][2]  
[How to][3]  
[UBUNTU 安装OPENVPN ][4]  


[1]: http://www.server-world.info/en/note?os=CentOS_6&p=openvpn
[2]: https://www.digitalocean.com/community/tutorials/how-to-setup-and-configure-an-openvpn-server-on-centos-6
[3]: http://openvpn.net/howto.html#pki
[4]: http://blog.csdn.net/tianxiajianling/article/details/7767119