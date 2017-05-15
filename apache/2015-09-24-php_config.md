# apache 中配置 php 解释器
apache2.4 和 php5.6 先安装好，这个就不说了

httpd.conf 中添加一条 include ，加载自定义配置，分开管理. cumtom目录自己建立

	Include conf/custom/*.conf
cumtom 目录中新建 php.conf, 添加以下内容（参照 xampp 配置， 没安装的话，对照这个文本吧）

	# php5 support
	LoadModule php5_module d:\software\php-5.6.13\php5apache2_4.dll
	AddType application/x-httpd-php .php
	# configure the path to php.ini
	PHPIniDir "d:/software/php-5.6.13"





## 错误处理

访问 http://localhost/index.php 报错， 打不开文件
>Warning: Unknown: failed to open stream: No such file or directory in Unknown on line 0

>Fatal error: Unknown: Failed opening required 'D:/eachcloud/我的坚果云/code/php/framework_study/index.php' (include_path='.;C:\php\pear') in Unknown on line 0



*注意事项*
1. php5.5 以上版本只能搭配 apache2.4以上, 新安装的话就不要用旧版本了

## 添加index类型，多添加几个

	<IfModule dir_module>
	    DirectoryIndex index.php index.pl index.cgi index.asp index.shtml index.html index.htm \
	                   default.php default.pl default.cgi default.asp default.shtml default.html default.htm \
	                   home.php home.pl home.cgi home.asp home.shtml home.html home.htm
	</IfModule>