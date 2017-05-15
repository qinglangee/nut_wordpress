# centos 软件安装
## git

	yum install git
## gcc
gcc and g++

	yum install gcc
	yum install gcc-c++
## node 

	# 先找到要安装版本的下载地址
	$ wget http://nodejs.org/dist/v0.10.29/node-v0.10.29.tar.gz .
	$ tar -xzf node-v0.10.29.tar.gz
	$ cd node-v0.10.29
	$ ./configure
	$ make

## nginx

	yum install zlib-devel wget openssl-devel pcre pcre-devel sudo gcc make autoconf automake
	cd download
	wget http://nginx.org/download/nginx-1.6.0.tar.gz .
	tar -xzf nginx-1.6.0.tar.gz
	cd nginx-1.6.0
	./configure   --user=nginx --group=nginx --with-http_ssl_module
	make && make install
	useradd -M -r --shell /bin/sh --home-dir /usr/local/nginx nginx     # /usr/local/nginx 是configure后显示的 nginx path prefix: "/usr/local/nginx"
*创建nginx启动脚本*

	#!/bin/sh
	#
	# nginx – this script starts and stops the nginx daemon
	#
	# chkconfig: - 85 15
	# description: Nginx is an HTTP(S) server, HTTP(S) reverse \
	# proxy and IMAP/POP3 proxy server
	# processname: nginx
	# config: /opt/nginx/conf/nginx.conf
	# pidfile: /opt/nginx/logs/nginx.pid

	# Source function library.
	. /etc/rc.d/init.d/functions

	# Source networking configuration.
	. /etc/sysconfig/network

	# Check that networking is up.
	[ "$NETWORKING" = "no" ] && exit 0

	nginx="/usr/local/nginx/sbin/nginx"
	prog=$(basename $nginx)

	NGINX_CONF_FILE="/usr/local/nginx/conf/nginx.conf"

	lockfile=/var/lock/subsys/nginx

	start() {
	    [ -x $nginx ] || exit 5
	    [ -f $NGINX_CONF_FILE ] || exit 6
	    echo -n $"Starting $prog: "
	    daemon $nginx -c $NGINX_CONF_FILE
	    retval=$?
	    echo
	    [ $retval -eq 0 ] && touch $lockfile
	    return $retval
	}

	stop() {
	    echo -n $"Stopping $prog: "
	    killproc $prog -QUIT
	    retval=$?
	    echo
	    [ $retval -eq 0 ] && rm -f $lockfile
	    return $retval
	}

	restart() {
	    configtest || return $?
	    stop
	    start
	}

	reload() {
	    configtest || return $?
	    echo -n $”Reloading $prog: ”
	    killproc $nginx -HUP
	    RETVAL=$?
	    echo
	}

	force_reload() {
	    restart
	}

	configtest() {
	    $nginx -t -c $NGINX_CONF_FILE
	}

	rh_status() {
	    status $prog
	}

	rh_status_q() {
	    rh_status >/dev/null 2>&1
	}

	case "$1" in
	    start)
	        rh_status_q && exit 0
	        $1
	        ;;
	    stop)
	        rh_status_q || exit 0
	        $1
	        ;;
	    restart|configtest)
	        $1
	        ;;
	    reload)
	        rh_status_q || exit 7
	        $1
	        ;;
	    force-reload)
	        force_reload
	        ;;
	    status)
	        rh_status
	        ;;
	    condrestart|try-restart)
	        rh_status_q || exit 0
	        ;;
	    *)
	        echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}"
	        exit 2
	esac

注册为服务

	chmod +x /etc/rc.d/init.d/nginx
	chkconfig --add nginx
	chkconfig nginx on
	service nginx start

## php 转发

	rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
	yum update
	yum install php-cli php spawn-fcgi
创建启动脚本
*vim /usr/bin/php-fastcgi*

	#!/bin/sh

	if [ `grep -c "nginx" /etc/passwd` = "1" ]; then
	   FASTCGI_USER=nginx
	elif [ `grep -c "www-data" /etc/passwd` = "1" ]; then
	   FASTCGI_USER=www-data
	elif [ `grep -c "http" /etc/passwd` = "1" ]; then
	   FASTCGI_USER=http
	else
	# Set the FASTCGI_USER variable below to the user that
	# you want to run the php-fastcgi processes as

	FASTCGI_USER=
	fi

	/usr/bin/spawn-fcgi -a 127.0.0.1 -p 9000 -C 6 -u $FASTCGI_USER -f /usr/bin/php-cgi

创建服务脚本

*vim  /etc/init.d/php-fastcgi*

	#!/bin/sh

	# php-fastcgi - Use php-fastcgi to run php applications
	#
	# chkconfig: - 85 15
	# description: Use php-fastcgi to run php applications
	# processname: php-fastcgi

	if [ `grep -c "nginx" /etc/passwd` = "1" ]; then
	   OWNER=nginx
	elif [ `grep -c "www-data" /etc/passwd` = "1" ]; then
	   OWNER=www-data
	elif [ `grep -c "http" /etc/passwd` = "1" ]; then
	   OWNER=http
	else
	# Set the OWNER variable below to the user that
	# you want to run the php-fastcgi processes as

	OWNER=
	fi

	PATH=/sbin:/bin:/usr/sbin:/usr/bin
	DAEMON=/usr/bin/php-fastcgi

	NAME=php-fastcgi
	DESC=php-fastcgi

	test -x $DAEMON || exit 0

	# Include php-fastcgi defaults if available
	if [ -f /etc/default/php-fastcgi ] ; then
	    . /etc/default/php-fastcgi
	fi

	set -e

	case "$1" in
	  start)
	    echo -n "Starting $DESC: "
	    sudo -u $OWNER $DAEMON
	    echo "$NAME."
	    ;;
	  stop)
	    echo -n "Stopping $DESC: "
	    killall -9 php-cgi
	    echo "$NAME."
	    ;;
	  restart)
	    echo -n "Restarting $DESC: "
	    killall -9 php-cgi
	    sleep 1
	    sudo -u $OWNER $DAEMON
	    echo "$NAME."
	    ;;
	      *)
	        N=/etc/init.d/$NAME
	        echo "Usage: $N {start|stop|restart}" >&2
	        exit 1
	        ;;
	    esac
	    exit 0
创建服务

	chmod +x /usr/bin/php-fastcgi
	chmod +x /etc/init.d/php-fastcgi
	service php-fastcgi start
	chkconfig --add php-fastcgi
	chkconfig php-fastcgi on

*编辑 /etc/sudoers 把 "Defaults    requiretty" 注释掉*

nginx配置转发

	location ~ \.php$ {
	    include /etc/nginx/fastcgi_params;
	    if ($uri !~ "^/images/") {
	    fastcgi_pass 127.0.0.1:9000;
	    }
	    fastcgi_index index.php;
	    fastcgi_param SCRIPT_FILENAME /srv/www/example.com/public_html$fastcgi_script_name;
	}

## mysql

	yum install mysql-server php-mysql

	/etc/rc.d/init.d/mysqld start
	chkconfig mysqld on
安全设置 

	mysql_secure_installation
创建用户和数据库

	create user 'username'@'%' identified by 'password';
	CREATE DATABASE `wordpress` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
	grant all on wordpress.* to  user_name@'%' identified by 'password';

*配置php-mysql*
`sudo find / -name php.ini -print | xargs echo` 可以找到php.ini的位置, 可能在 /etc/php.ini
打开php.ini, 在[MySQL]的下面加一行

	extension=mysql.so
然后重启php-fastcgi

	service php-fastcgi restart

	
## wordpress
下载解压到 nginx server的root目录  
[5分钟安装][2]

*wordpress目录不能放在/root目录下,nginx会报403 forbidden, 可以放到/srv或/home/user等目录下*



[LEMP Server on CentOS 6][1]


[1]: https://library.linode.com/lemp-guides/centos-6
[2]: http://codex.wordpress.org/Installing_WordPress#Famous_5-Minute_Install