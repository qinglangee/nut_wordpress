# ubuntu 安装 mysql server

## 安装MySQL

要安装 MySQL，可以在终端提示符后运行下列命令：

	sudo apt-get install mysql-server mysql-client #中途会让你输入一次root用户密码
	sudo apt-get install php5-mysql  #安装php5-mysql 是将php和mysql连接起来

一旦安装完成，MySQL 服务器应该自动启动。

	sudo start mysql #手动的话这样启动
	sudo stop mysql #手动停止

当你修改了配置文件後，你需要重启 mysqld 才能使这些修改生效。

要想检查 mysqld 进程是否已经开启，可以使用下面的命令：

	pgrep mysqld

如果进程开启，这个命令将会返回该进程的 id。 

## 文件结构

MySQL配置文件：/etc/mysql/my.cnf ，其中指定了数据文件存放路径

	datadir         = /var/lib/mysql

如果你创建了一个名为 test 的数据库，那么这个数据库的数据会存放到 /var/lib/mysql/test 目录下。 
## 进入MySQL

	mysql -u root -p 

修改 MySQL 的管理员密码：

	sudo mysqladmin -u root password newpassword；

## 设置远程访问

1.取消本地监听
正常情况下，mysql占用的3306端口只是在IP 127.0.0.1上监听，拒绝了其他IP的访问（通过netstat可以查看到）。取消本地监听需要修改 my.cnf 文件：

	sudo vim /etc/mysql/my.cnf
	//找到如下内容，并注释
	bind-address = 127.0.0.1

然后需要重启 mysql （可最后再重启）。

2.授权法

	mysql>GRANT ALL PRIVILEGES ON *.* TO <user>@"%" IDENTIFIED BY '<password>' WITH GRANT OPTION;
	mysql>FLUSH PRIVILEGES

第二句表示从mysql数据库的grant表中重新加载权限数据。因为MySQL把权限都放在了cache中，所以在做完更改后需要重新加载。 




refs:  


[ubuntu mysql wiki](http://wiki.ubuntu.com.cn/MySQL)
