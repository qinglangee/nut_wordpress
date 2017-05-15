# mysql 编码

## character-set-server
如果不设置这两个值的话下面就是默认值，`character-set-server` 就是在数据库 character set 和 collation 没指定时的默认值， 没有其它用途。

	mysqld --character-set-server=latin1    --collation-server=latin1_swedish_ci
## 数据库 char set 和 collation
数据库创建和修改时可以指定 char set 和 collation

	CREATE DATABASE db_name
	    [[DEFAULT] CHARACTER SET charset_name]
	    [[DEFAULT] COLLATE collation_name]

	ALTER DATABASE db_name
	    [[DEFAULT] CHARACTER SET charset_name]
	    [[DEFAULT] COLLATE collation_name]

The keyword SCHEMA can be used instead of DATABASE. All database options are stored in a text file named db.opt that can be found in the database directory.

实例：

	CREATE DATABASE db_name CHARACTER SET latin1 COLLATE latin1_swedish_ci;

## 表级别和字段级别的 char set 和 collation
这个也可以实现， 但还是不要搞了， 弄那么乱没什么意思 。


## 客户端乱码
在数据库 utf8, 中文系统客户端乱码时，试一下

	set names gb2312;
这个是因为服务端的默认编码不是UTF8, 两端不统一造成的， 更好的解决方法就是所有端都统一为utf8.

`my.ini` 配置文件中， client,mysql,mysqld中都修改或添加 utf8字符设置


	[client]
	port=3306
	default-character-set=utf8
	[mysql]
	default-character-set=utf8
	[mysqld]
	character-set-server=utf8

## 查看字符的相关设置

	SHOW VARIABLES LIKE 'character_set_%';
	SHOW VARIABLES LIKE 'collation_%';

refs:  
[10.1.3.1 Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.6/en/charset-server.html)  


[1]: http://dev.mysql.com/doc/refman/5.6/en/charset-database.html