# linux 远程挂载目录

## 一 NFS 服务
Network Files Service
RPC (Remote Procedure Call) 

## 二 系统环境

系统平台：CentOS7或RHEL7
NFS Server IP：172.25.0.11
防火墙已:关闭或这允许NFS
SELINUX=disabled

## 三 安装NFS服务

    nfs-utils ：包括基本的NFS命令与监控程序
    rpcbind ：支持安全NFS RPC服务的连接

	# yum install nfs-utils portmap  （适用centos 5）
	# yum install nfs-utils rpcbind  （适用centos 6/7）
## 四NFS系统守护进程

1. nfsd：它是基本的NFS守护进程,主要功能是管理客户端是否能够登录服务器；
2. mountd：它是RPC安装守护进程,主要功能是管理NFS的文件系统。当客户端顺利通过nfsd登录NFS服务器后,在使用NFS服务所提供的文件前,还必须通过文件使用权限的验证。它会读取NFS的配置文件/etc/exports来对比客户端权限。
3. rpcbind：主要功能是进行端口映射工作。当客户端尝试连接并使用RPC服务器提供的服务（如NFS服务）时,rpcbind会将所管理的与服务对应的端口提供给客户端,从而使客户可以通过该端口向服务器请求服务。

## 五、NFS服务器的配置

NFS服务器的配置相对比较简单,只需要在相应的配置文件中进行设置,然后启动NFS服务器即可。

NFS的常用目录
 
/etc/exports                            NFS服务的主要配置文件
/usr/sbin/exportfs                      NFS服务的管理命令
/usr/sbin/showmount                     客户端的查看命令
/var/lib/nfs/etab                       记录NFS分享出来的目录的完整权限设定值
/var/lib/nfs/xtab                       记录曾经登录过的客户端信息

NFS服务的配置文件为 /etc/exports, 这个文件是NFS的主要配置文件,不过系统并没有默认值,所以这个文件不一定会存在,可能要使用vim手动建立,然后在文件里面写入配置内容。

/etc/exports文件内容格式：
 

	<输出目录> [客户端1 选项（访问权限,用户映射,其他）] [客户端2 选项（访问权限,用户映射,其他）]

a. 输出目录： 输出目录是指NFS系统中需要共享给客户机使用的目录；

b. 客户端： 客户端是指网络中可以访问这个NFS输出目录的计算机

客户端常用的指定方式

指定ip地址的主机：192.168.0.200
指定子网中的所有主机：192.168.0.0/24 192.168.0.0/255.255.255.0
指定域名的主机：nfs.cnhzz.com
指定域中的所有主机：*.cnhzz.com
所有主机：*

c. 选项：选项用来设置输出目录的访问权限、用户映射等。

NFS主要有3类选项：

访问权限选项

    设置输出目录只读：ro
    设置输出目录读写：rw

用户映射选项

    all_squash：将远程访问的所有普通用户及所属组都映射为匿名用户或用户组（nfsnobody）；
    no_all_squash：与all_squash取反（默认设置）；
    root_squash：将root用户及所属组都映射为匿名用户或用户组（默认设置）；
    no_root_squash：与rootsquash取反；
    anonuid=xxx：将远程访问的所有用户都映射为匿名用户,并指定该用户为本地用户（UID=xxx）；
    anongid=xxx：将远程访问的所有用户组都映射为匿名用户组账户,并指定该匿名用户组账户为本地用户组账户（GID=xxx）；

其它选项

    secure：限制客户端只能从小于1024的tcp/ip端口连接nfs服务器（默认设置）；
    insecure：允许客户端从大于1024的tcp/ip端口连接服务器；
    sync：将数据同步写入内存缓冲区与磁盘中,效率低,但可以保证数据的一致性；
    async：将数据先保存在内存缓冲区中,必要时才写入磁盘；
    wdelay：检查是否有相关的写操作,如果有则将这些写操作一起执行,这样可以提高效率（默认设置）；
    no_wdelay：若有写操作则立即执行,应与sync配合使用；
    subtree：若输出目录是一个子目录,则nfs服务器将检查其父目录的权限(默认设置)；
    no_subtree：即使输出目录是一个子目录,nfs服务器也不检查其父目录的权限,这样可以提高效率；


## 防火墙配置
由于nfs服务需要开启 mountd,nfs,nlockmgr,portmapper,rquotad这5个服务，需要将这5个服务的端口加到iptables里面 *centos7里面好像没有rquotad服务了*

而nfs 和 portmapper两个服务是固定端口的，nfs为2049，portmapper为111。其他的3个服务是用的随机端口，那就需要先把这3个服务的端口设置成固定的。  
用 `rpcinfo -p`命令查看这几个服务用到的端口号，记下来

>[root@localhost classes]# rpcinfo -p
program vers proto   port  service
100000    4   tcp    111  portmapper
100000    3   tcp    111  portmapper
100000    2   tcp    111  portmapper
100000    4   udp    111  portmapper
100000    3   udp    111  portmapper
100000    2   udp    111  portmapper
100024    1   udp  32985  status
100024    1   tcp  55645  status
100005    1   udp  20048  mountd
100005    1   tcp  20048  mountd
100005    2   udp  20048  mountd
100005    2   tcp  20048  mountd
100005    3   udp  20048  mountd
100005    3   tcp  20048  mountd
100003    3   tcp   2049  nfs
100003    4   tcp   2049  nfs
100227    3   tcp   2049  nfs_acl
100003    3   udp   2049  nfs
100003    4   udp   2049  nfs
100227    3   udp   2049  nfs_acl
100021    1   udp  34000  nlockmgr
100021    3   udp  34000  nlockmgr
100021    4   udp  34000  nlockmgr
100021    1   tcp  54584  nlockmgr
100021    3   tcp  54584  nlockmgr
100021    4   tcp  54584  nlockmgr

在 /etc/services 文件中固定服务的端口号， rquotad 没有就不用加了

     在文件的最后一行添加：

     mountd  20048/tcp
     mountd  20048/udp
     nlockmgr 54584/tcp
     nlockmgr 34000/udp

     rquotad  966/tcp
     rquotad  966/udp
*centos7 中发现 nlockmgr用这种方法不能固定端口号* 

/etc/sysconfig/nfs 中有配置 但不起作用，通过 `/usr/lib/systemd/scripts/nfs-utils_env.sh` 中的提示，直接写到`/etc/sysctl.conf`中

	# echo -e '###NFS ADD\nfs.nfs.nlm_tcpport = 32803\nfs.nfs.nlm_udpport = 32769' >> /etc/sysctl.conf
	# sysctl -p
再重启 nfs 服务端口就全固定了。

编辑iptables配置文件  

     vim /etc/sysconfig/iptables
添加如下行：

	# tcp part
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p tcp --dport 111 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p tcp --dport 976 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p tcp --dport 2049 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p tcp --dport 966 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p tcp --dport 33993 -j ACCEPT

	 

	# udp part
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p udp --dport 111 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p udp --dport 976 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p udp --dport 2049 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p udp --dport 966 -j ACCEPT
	-A INPUT -s 192.168.0.0/24 -m state --state NEW -p udp --dport 33993 -j ACCEPT

保存退出并重启iptables

	service iptables restart


refs:  
[centos7和rhel7的NFS服务器安装与配置](http://linux.it.net.cn/CentOS/course/2016/0330/20886.html)  
[linux服务器 NFS + 防火墙配置 ](http://blog.csdn.net/lincy100/article/details/6417743)  
[Linux之CentOS 7 上NFS共享服务器iptables 规则写法](https://www.dwhd.org/20160614_110518.html)  
