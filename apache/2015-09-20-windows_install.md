# windows 安装 apache

apache 项目不提供 windows 的二进制安装包，[ApacheHaus][1]， Apache Lounge 有提供编译好的二进制文件，Apache Lounge 提供的运行时报缺少什么DLL文件，就不用它了。

ApacheHaus 页面提供的下载，解压就能用。 它的说明文档里说要安装 [Visual C++ 2012 x64 Redistributable Package][2]，反正没安装时也能运行，也可能是以前装别的软件时安装过了。

运行前要设置一下 httpd.conf,  SRVROOT 设为 apache 的解压目录。 *目录后面不要加斜杠，目录分隔用斜杠，不要用反斜杠*
`Define SRVROOT "d:/software/Apache24"`  

`Cannot load modules/mod_actions.so into server` 之类的错误就是因为 SRVROOT 设置得不对， httpd 通过相对目录找不到需要的 moudle 文件。

## 安装 apache 为服务

	httpd -k install
启动服务，后台运行 `httpd -k start`  

安装为服务后，也可以通过 ApacheMonitor 来启动、重启、关闭。

一些其它命令

	Stop Apache	 	httpd -k stop
	Restart Apache	httpd -k restart
	Uninstall Apache Service	httpd -k uninstall
	Test Config Syntax	httpd -t
	Version Details	httpd -V
	Command Line Options List	httpd -h






[1]: http://www.apachehaus.com/cgi-bin/download.plx
[2]: http://www.microsoft.com/en-us/download/details.aspx?id=30679 