# mysql 数据库改名

MySQL数据库改名


某项目中有需求要将数据库改个名字，从MySQL的参考手册中发现有rename database的SQL命令，兴冲冲的执行了

mysql> rename database db1 to db2;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use n
r 'database db1 to db2' at line 1


查了一下，发现这条命令在MySQL 5.1.7的时候被添加进来，5.1.23的时候又被去掉了，查了一下版本：

 mysql> select @@version;
| @@version |
+-----------+
| 5.5.23 |
+-----------+


再想其他办法，查了一些资料以后总结如下：

1、MYISAM引擎把库名字对应的文件夹名改了

1.1、关闭mysqld

1.2、把data目录中的db_name目录重命名为new_db_name

1.3、打开mysqld


2、INNODB引擎分为下面几个步骤：

2.1 按新名字建立一个数据库

2.2 删除原有库中所有表上的触发器

2.3 使用rename table命令将表从原数据库复制到新数据库

2.4 在新数据库上重新创建2.2中被删除的触发器

2.5 在新数据库上重新创建存储过程、自定义函数、Events等


RENAME TABLE命令语法：

RENAME TABLE db_name.table1 TO new_db_name.table1,
                     db_name.table2 TO new_db_name.table2;


copied from:  
[MySQL数据库改名](http://blog.csdn.net/ghlfllz/article/details/8092068)  