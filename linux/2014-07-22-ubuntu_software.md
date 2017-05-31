# ubuntu 软件安装

## pidgin

更新ubuntu的pidgin  PPA

  1. 下载[Pidgin PPA package][2].
  2. 安装.
  3. sudo apt-get update
  4. sudo apt-get install pidgin
[pidgin office site for ubuntu][1]  

## zsh 

	sudo apt-get install zsh
## Nutstore 坚果云
先看[官方的安装文档][3]有没有更新, 没有就照这儿的来.  
依赖的有这些, 装了的就不用再装了

	sudo apt-get install openjdk-6-jre-headless gvfs-bin python-notify
64位下载文件

	wget http://jianguoyun.com/static/exe/installer/nutstore_linux_dist_x64.tar.gz -O /tmp/nutstore_bin.tar.gz
创建需要的目录
	
	mkdir -p ~/.nutstore/dist && tar zxf /tmp/nutstore_bin.tar.gz -C ~/.nutstore/dist
然后安装

	~/.nutstore/dist/bin/install_core.sh
## apache2

	sudo apt-get install apache2
重装, [先带配置文件全删了, 再重装][4],  [另一篇][5]

	sudo apt-get remove --purge apache2
	sudo apt-get install apache2


[1]: http://pidgin.im/download/ubuntu/
[2]: https://launchpad.net/~pidgin-developers/+archive/ppa/+files/pidgin-ppa_0.0.7_all.deb
[3]: https://jianguoyun.com/s/downloads/linux#install_for_kdexfce
[4]: http://yang900604.blog.163.com/blog/static/95534672201281505453239/
[5]: http://www.vpsa.net/?post=40