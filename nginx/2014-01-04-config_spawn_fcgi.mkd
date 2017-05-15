#  nginx配置spawn-fcgi

## 下载
http://redmine.lighttpd.net/projects/spawn-fcgi/wiki
选择一个版本下载

## 安装
./configure
make
make install

## 配置
[这里有一个nginx配置php-cgi的例子](http://wiki.nginx.org/PHPFcgiExampleOld)
既然这样那么就先用php-cgi吧
php-cgi -b 127.0.0.1:9000

这个服务如果被关掉了的话，访问页面就ger pi了


有个问题是本来nginx.conf中是用nginx用户的, 老是报403 forbidden, 改成用root用户后就可以了.

配置完之后刚好有文章时说的那个错误, No input file specified, 但照它说的设置了下不起作用. 
怎么会这样呢, 再后来又看了一下, 还是设置的错了, root要放在最外层, 不能放在别的location里面, 要不就对别的location不起作用了.

