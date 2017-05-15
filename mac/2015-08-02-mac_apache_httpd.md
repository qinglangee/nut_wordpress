# osx 下的自带 apache
## apache

打开终端，运行
启动 Apache 命令： 
`sudo apachectl start`
关闭命令： 
`sudo apachectl stop`
重启命令： 
`sudo apachectl restart`
查看 Apache 版本命令： 
`httpd -v`

OS X 中默认有两个目录可以直接运行你的 Web 程序，一个是系统级的 Web 根目录，一个是用户级的根目录，大家记下即可。 
系统级的根目录是： 
/Library/WebServer/Documents/
它对应的网址是： 
http://localhost
用户级的根目录是： 
~/Sites

~/Sites 也就是你用户目录下面的”站点”目录，在 OS X Mountain Lion 中，这个目录可能没有，所以你需要手动建立一个同名目录。建立方式很简单，直接在终端中运行： 
sudo mkdir ~/Sites
建立”站点”文件夹之后，检查下面这个文件夹下面是不是有”你的用户名.conf”这个文件。 
/etc/apache2/users/
如果没有，那么你需要创建一个，取名为”你的用户名.conf”，你可以使用 vi 或者 nano 这两种编辑器之一来创建。 
sudo vi /etc/apache2/users/你的用户名.conf
创建之后将下面的这几行内容写到上面的 conf 文件中： 
<Directory "/Users/username/Sites/">
Options Indexes MultiViews
AllowOverride All
Order allow,deny
Allow from all
</Directory>
文件保存之后，给它赋予相应的权限： 
sudo chmod 755 /etc/apache2/users/你的用户名.conf
接下来重启 Apache，以使该配置文件生效： 
sudo apachectl restart
之后你就可以通过浏览器访问你的用户级目录网页了，你可以随便防个网页进去测试一下。根目录地址为： 
http://localhost/~username/
(请将username改成你的用户名) 
启用 PHP 
Mountain Lion 中已经集成了 PHP 5.3.13 版本，也需要手动开启。你可以用 vi 或者 nano 编辑器打开下面这个文件： 
sudo nano /etc/apache2/httpd.conf
然后搜索”php”，第一条匹配的应该是下面这句代码： 
LoadModule php5_module libexec/apache2/libphp5.so 
请将这句代码前面的#去掉，然后保存文件。 
接下来再一次重启 Apache： 
sudo apachectl restart
现在 PHP 应该已经开始工作了，你可以在用户级根目录下(~/Sites/)放一个PHP测试文件，代码如下： 
<?php phpinfo(); ?>