# apache 服务器配置 php

## 安装 apache 服务器
Macos 自带的  `sudo apachectl start`

Ubuntu 自带的 `sudo service apache2 start`

## apache 配置 php
php 在 *nix 系统一般都自带的

Ubuntu 下 `/etc/apache2/mods-available` 中 php 相关配置 cp 到 `mods-available` 目录中.   
文件内容差不多就是:  
 	
	LoadModule php5_module modules/libphp5.so
应该就可以了.  

后面还做了两步, 因为 Hello World. 程序写错了, 不知道是不是需要的. 

1. 一个是 `sudo apt-get install libapache2-mod-php5` 安装了一个 apache-php 模块, 这个应该是之前就安装过.
2. 另一个是 `VirtualHost` 元素中添加 `FilesMatch`, 为了安全因素. 详见[php apache doc][1]. 

代码如下:

	<VirtualHost *:80>
	ServerName ppp.l99.com
	DocumentRoot /home/lifeix/Documents/apache_doc_root/ppp_root
	#Rewriteloglevel 1
	#Rewritelog /var/log/apache2/ppp.l99.rewrite.log
	    <FilesMatch "\.(php*|phtm|phtml|asp|aspx)$">
	    SetHandler application/x-httpd-php
	    </FilesMatch>

	</VirtualHost>




refs:  
[php apache doc][1]
[Apache 2.x on Unix systems](http://php.net/manual/en/install.unix.apache2.php)  


[1]: http://php.net/manual/en/book.apache.php