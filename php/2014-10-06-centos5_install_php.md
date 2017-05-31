# 在centos 5.5 下编译安装 php5.6

## yum 安装 php

*如果 只是要安装php 5.3 版本, 可以参照 zabbix 安装, 安装 zabbix安装源后, yum 安装 zabbix-web时会依赖安装php53*


## 安装前准备
去掉旧的php及扩展

	yum remove php php-common php-devel php-cli php-mbstring php-mhash php-mysql php-pgsql php-ldap php-imap php-pear php-pdo php-gd
安装需要的依赖, 如果不需要pgsql数据库则可以去掉postgresql相关包

	# yum install httpd-devel libtool-ltdl libtool-ltdl-devel openssl-devel \
	libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel \
	libc-client libc-client-devel gd gd-devel libmcrypt libmcrypt-devel \
	sqlite sqlite-devel mysql-devel libicu libicu-devel pcre-devel \

	libxml2 libxml2-devel curl-devel gmp gmp-devel \

	postgresql84 postgresql84-libs postgresql84-server postgresql84-devel \

如果不安装 libtool-ltdl-devel编译时会出错，所以要么安装这个包要么执行以下命令：

	# cd /usr/lib
	# ln -s libltdl.so.3.1.4 libltdl.so
libicu是 --enable-intl Enable internationalization support 需要的包

## 下载源码 [下载](http://php.net/downloads.php)

*php-5.6.1.tar.gz*

## 解压 && 安装

配置安装参数

	./configure --build=i686-RedHat-linux-gnu --host=i686-redhat-linux-gnu --target=i686-RedHat-linux-gnu \
	--with-pgsql --with-pdo-pgsql \

	--with-apxs2=/usr/sbin/apxs \
	--prefix=/usr/local --exec-prefix=/usr/local --with-exec-dir=/usr/local/bin \
	--sysconfdir=/etc --libdir=/usr/local/lib/php --with-libdir=lib \
	--sbindir=/usr/local/sbin --sharedstatedir=/usr/com --datadir=/usr/local/share \
	--includedir=/usr/local/include --libexecdir=/usr/local/libexec \
	--localstatedir=/var --cache-file=../config.cache \
	--mandir=/usr/local/share/man --infodir=/usr/local/share/info \
	--with-config-file-path=/etc --with-config-file-scan-dir=/etc/php.d \
	--with-pic --with-curl=shared --with-freetype-dir --with-png-dir \
	--with-gettext --with-gmp --with-iconv --with-jpeg-dir --with-png-dir \
	--with-openssl --with-layout=GNU --with-libxml-dir \
	--with-pcre-regex=/usr \
	--with-mcrypt=shared --with-mhash --with-zlib --with-bz2=shared \
	--with-pdo-mysql --with-mysql --with-mysql-sock=/var/lib/mysql/mysql.sock \
	--with-sqlite=shared --with-pdo-sqlite=shared \
	--enable-sqlite-utf8 --with-kerberos --with-imap --with-imap-ssl \
	--with-pear --with-gd --enable-gd-native-ttf --enable-calendar=shared \
	--enable-exif --enable-ftp --enable-sockets --enable-bcmath \
	--enable-sysvsem --enable-sysvshm --enable-sysvmsg --enable-intl \
	--enable-mbstring --enable-zend-multibyte --enable-zip \
	--without-unixODBC --disable-tokenizer
解决配置中的错误 , 然后 

	make
	make install
	
*安装中报错*
>checking for xml2-config path... 
configure: error: xml2-config not found. Please check your libxml2 installation.

这个是因为 libxml2 libxml2-devel 没有安装, 把这两个装上就好了. 

	yum install  libxml2 libxml2-devel

>checking for cURL in default path... not found
>configure: error: Please reinstall the libcurl distribution -
>    easy.h should be in <curl-dir>/include/curl/

curl的devel包没有安装

	yum -y install curl-devel
>configure: error: cannot run test program while cross compiling

把  --build=i686-RedHat-linux-gnu --host=i686-redhat-linux-gnu --target=i686-RedHat-linux-gnu  这几个选项去掉
>configure: error: Unable to locate gmp.h

	yum install gmp gmp-devel 
>configure: error: ICU version 4.0 or later is required

没找到解决方法 , 把依赖它的  --enable-intl 参数去掉了.
>configure: error: Cannot find libpq-fe.h. Please specify correct PostgreSQL installation path

把 pgsql相关的参数去掉

refs:  
[CentOS 5.5上编译安装 PHP 5.3.6][1]  
[PHP编译安装错误:configure:error:xml2-config not found的解法方法][2]  
[解决configure: error: Please reinstall the libcurl distribution][3]  
[[转] error: cannot run test program while cross compiling ][4]   



[1]: http://www.myhack58.com/Article/sort099/sort0102/2011/30174.htm
[2]: http://blog.163.com/linshengru@126/blog/static/9866379420111190353230/
[3]: http://150588fw.blog.163.com/blog/static/467849442009112105128810/
[4]: http://tassardge.blog.163.com/blog/static/1723017082010111554018645/