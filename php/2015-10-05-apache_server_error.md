# apache 常见错误

## Warning: Unknown: failed to open stream: No such file or directory in Unknown on line 0

>Warning: Unknown: failed to open stream: No such file or directory in Unknown on line 0
>
>Fatal error: Unknown: Failed opening required 'E:/php/www/mrsoft/注册登录模块/index.php' (include_path='.;C:\php5\pear') in Unknown on line 0

分析：
      apache不能解析含中文路径的url，只要把上面的中文路径（“注册登录模块”）改成英文的就行。。。

## Forbidden

>Forbidden
>
>You don't have permission to access /index.php on this server.

httpd.conf 查找一下 deny 相关的设置，改为正确的配置

	<Directory />
	    # AllowOverride none
	    # Require all denied

	    Options FollowSymLinks
	    AllowOverride None
	</Directory>