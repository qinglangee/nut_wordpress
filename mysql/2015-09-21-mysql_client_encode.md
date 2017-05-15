# mysql 客户端连接编码问题

## mysql 客户端乱码

症状：在终端可以正常查询、插入中文，在客户端显示乱码。

首先在在终端和客户端输入：

	SHOW VARIABLES LIKE 'CHAR%';
正确的显示应该是：

+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+


如果有latin-1

    vi  /etc/mysql/my.cnf
插入default-character-set   = utf8到[client]和[mysqld]内（注意：windows下5.5.8中[mysqld]中应变成：character-set-server = utf8）。
然后重启mysql服务，默认字符编码就是utf8了。(CMD下先chcp 65001，再登陆mysql，可避免客户端字符集为gbk)

但是客户端执行
USE SCHEMATA;
SHOW VARIABLES LIKE 'CHAR%';
却可能会看到latin-1
这种情况多半都是建立库、表的时候没有设置utf8编码。要么删了重建，要么修改。
于是google到了 mysql 数据库 表 字段 编码修改 方法
修改库编码为utf8

    ALTER DATABASE `test` DEFAULT CHARACTER SET utf8 COLLATE utf8_bin
修改表编码为utf8

    ALTER TABLE `category` DEFAULT CHARACTER SET utf8 COLLATE utf8_bin
修改字段编码为utf8

    ALTER TABLE `test` CHANGE `dd` `dd` VARCHAR( 45 ) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL

当然，如果你导入数据的时候是latin-1，修改之后反而会乱码……所以，我选择删掉重新导入！
google到两篇很不错的文章，感谢他们分享，有需要的朋友可以看看，写得非常详细。
[mysql 数据库 表 字段 编码修改 方法][1]  
[MySQL 中文显示乱码][2]  


*查看单个表的字符设置*

    show full columns from table_name;





refs:  
[解决MySQL 客户端中文乱码  ](http://blog.163.com/wmkq_cq/blog/static/16958236420112611514437/)  


## [mysql 中文显示乱码][2]  的备份

最近关于中文显示乱码的贴子比较多，所以也做了个总结：

可以参考一下杨涛涛版主的《各种乱码问题汇总》
http://topic.csdn.net/u/20071124/08/3b7eae69-ed1d-4a77-8895-9930bf3601af.html

MySQL字符集的原理介绍。摘录于官方文档。http://dev.mysql.com/doc/refman/5.1/zh/charset.html

不同的编码格式会导致同一字符，在不同字符集下的编码会不同。同样同一编码在不同的字符集中代码的字符也不相同。当你的MySQL返回的字符串的编码格式（字符集）与你的客户工具程序（mysql, php, query browser, ...）当前使用的字符集不同时，就会造成乱码。 比如一个英国朋友告诉你Long, 当一位中国小学生看到后就会告诉你“龙”而不是“长”

关于字符集的详细介绍和例子，建议花一点时间看一下
http://dev.mysql.com/doc/refman/5.1/zh/charset.html  (第10章：字符集支持)。


这里仅摘要一下。

MySQL中默认字符集的设置有四级:服务器级，数据库级，表级 。最终是字段级 的字符集设置。注意前三种均为默认设置，并不代码你的字段最终会使用这个字符集设置。所以我们建议要用show create table table ; 或show full fields from tableName; 来检查当前表中字段的字符集设置。

MySQL中关于连接环境的字符集设置有  Client端，connection, results 通过这些参数，MySQL就知道你的客户端工具用的是什么字符集，结果集应该是什么字符集。这样MySQL就会做必要的翻译，一旦这些参数有误，自然会导致字符串在转输过程中的转换错误。基本上99%的乱码由些造成。

乱码后需要检查的信息。(如果需要论坛上的朋友帮助，建议你提供以下信息 )


1. 数据库表中字段的字符集设置 。show create table TableName 或 show full columns from tableName


mysql> show create table t1;
+-------+------------------------------------
| Table | Create Table                      
+-------+------------------------------------
| t1    | CREATE TABLE `t1` (
  `id` int(11) NOT NULL,
  `c1` varchar(30) DEFAULT NULL,
  PRIMARY KEY (`id`)   
) ENGINE=InnoDB DEFAULT CHARSET=gbk |
+-------+------------------------------------
1 row in set (0.00 sec)
                       
mysql> show full columns from t1;
+-------+-------------+----------------+------+-----+-
| Field | Type        | Collation      | Null | Key |
+-------+-------------+----------------+------+-----+-
| id    | int(11)     | NULL           | NO   | PRI |
| c1    | varchar(30) | gbk_chinese_ci | YES  |     |
+-------+-------------+----------------+------+-----+-
2 rows in set (0.00 sec)
mysql>

 

2. 当前联接系统参数  show variables like 'char%'


mysql> show variables like 'char%';
+--------------------------+----------------
| Variable_name            | Value
+--------------------------+----------------
| character_set_client     | gbk
| character_set_connection | gbk
| character_set_database   | latin1
| character_set_filesystem | binary
| character_set_results    | gbk
| character_set_server     | latin1
| character_set_system     | utf8
| character_sets_dir       | C:/Program File
+--------------------------+----------------
8 rows in set (0.00 sec)


  mysql>


1. 中文，请确保 表中该字段的字符集为中文兼容：
 big5     | Big5 Traditional Chinese
 gb2312   | GB2312 Simplified Chinese
 gbk      | GBK Simplified Chinese
 utf8     | UTF-8 Unicode

 

2. 确保，联接参数与这个字段字符集一致,你可以用 set name 'charsetname';
 比如， set name 'gbk';
 这条命令会同时修改 character_set_client,character_set_connection,character_set_results
 (如果你的这架MySQL中都为中文，则你可以在my.ini或my.cnf中加上或修改这个参数, 参数文件修改后需重启MySQL服务)
[mysql]
default-character-set=gbk

 

3. PHP 乱码, 同样 mysql_query("set name 'gbk'"); 其它API也类似。

 

4. phpmyadmin里乱码
phpMyAdmin的config.inc.php中有没有设置$cfg['DefaultCharset']='utf-8';

 

5. Windows操作系统中命令行（"DOS"窗口)下。
 在你的DOS窗中的左上角标题栏片左键，属性，
 在字体中，选择“宋体”，确认
 mysql中 set names 'gbk';

 

6. ADO.NET, ADO中 ，可以连接字符串中加入CharSet=UTF8;类似指令以说明connection的字符集。
 Server=myServerAddress;Database=myDataBase;Uid=myUsername;Pwd=myPassword; CharSet=UTF8;

 

7. SQL Manager for MySQL

用EMS建数据库，

 Character Set设为utf-8

 client charset设UTF-8

 Font charset 设为GB2312_CHARSET


8. jdbcodbc桥接 http://java.sun.com/j2se/1.4.2/docs/guide/jdbc/bridge.html

       // Load the JDBC-ODBC bridge driver
       Class.forName(sun.jdbc.odbc.JdbcOdbcDriver) ;

       // setup the properties
       java.util.Properties prop = new java.util.Properties();
       prop.put( " charSet " , " Big5 " );
       prop.put( " user " , username);
       prop.put( " password " , password);

       // Connect to the database
       con = DriverManager.getConnection(url, prop);

 

9.  PHP 5.2 版本以上解决乱码问题的一个方法 (由 ljf_ljf [Mark Liang] 提供)

    $conn = mysql_connect ( " 192.168.1.133 " , " root " , " 123456 " ) or
        die ( " Could not connect: " . mysql_error ());

    $program_char = " utf8 " ;

    $conn . mysql_select_db ( " test " );
    // $conn.mysql_query('SET @@character_set_results = "'.$program_char.'"');
   
    mysql_set_charset( $program_char , $conn );
    $charset = mysql_client_encoding ( $conn );
    printf ( " current character set is %s <br> " , $charset );
    $result = mysql_query ( " SELECT id, task_no,pack_path FROM tb_workplan where id = 1 " , $conn );
    while ( $row = mysql_fetch_array ( $result , MYSQL_BOTH)) {
        printf ( " ID: %s <br> task_no: %s  <br> pack_path :%s <BR> " , $row [ " id " ] , $row [ 1 ] , $row [ " pack_path " ]); 
    }
    $conn . mysql_free_result ( $result );
    $conn . mysql_close ();

 

9.  存储过程参数乱码

create procedure t ( aa char(10) charset 'gbk')

未完。。。


[1]: http://okone96.itpub.net/post/9033/403771 
[2]: http://blog.csdn.net/ACMAIN_CHM/article/details/4174186
