# c++ 使用 sqlite

[谈一谈sqlite这种小型数据库（1）](https://www.cnblogs.com/bwbfight/p/9306293.html)  
[谈一谈sqlite这种小型数据库（2）](https://www.cnblogs.com/bwbfight/p/9307617.html)  
[C++ Sqlite3的基本使用](https://www.cnblogs.com/KillerAery/p/9114124.html)  
[runoob 上的 SQLite - C/C++接口教程](https://www.runoob.com/sqlite/sqlite-c-cpp.html)  


# 文件组织
在 sqlite 官网下载页面可以下载命令行工具，用以在命令行操作数据库。 

## 用源文件编译内嵌 sqlite
下载 sqlite-amalgamation-xxxxxxxx.zip, 把 sqlite3.c 和 sqlite3.h 放到项目里就可以编译使用了。

## 编译出lib使用
跟上面一样，自己编译出 lib , 包含 sqlite3.h ，指明 lib 位置使用就行了

## 使用 dll 导入使用
TODO 


# 代码接口

## 核心对象

在SQLite中最主要的两个对象是，database_connection和prepared_statement.  
database_connection对象是由sqlite3_open()接口函数创建并返回的，在应用程序使用任何其 他SQLite接口函数之前，必须先调用该函数以便获得database_connnection对象，在随后的 其他APIs调用中，都需要该对象作为输入参数以完成相应的工作。  
至于prepare_statement， 我们可以简单的将它视为编译后的SQL语句，因此，所有和SQL语句执行相关的函数也都需要 该对象作为输入参数以完成指定的SQL操作

## 接口
1). sqlite3_open
2). sqlite3_prepare
3). sqlite3_step
4). sqlite3_column

　　该函数用于获取当前行指定列的数据，然而严格意义上讲，此函数在SQLite的接口函 数中并不存在，而是由一组相关的接口函数来完成该功能，其中每个函数都返回不同 类型的数据

如： sqlite3_column_blob  

　　 sqlite3_column_bytes  

　　sqlite3_column_bytes16

　　sqlite3_column_double

　　sqlite3_column_int

　　sqlite3_column_int64

　　 sqlite3_column_text

　　sqlite3_column_text16

　　sqlite3_column_type

　　 sqlite3_column_value

　　 sqlite3_column_count

　　 其中sqlite3_column_count函数用于获取当前结果集中的字段数据。下面是使用 sqlite3_step和sqlite3_column函数迭代结果集中每行数据的伪代码，注意这里作为示 例代码简化了对字段类型的判断：
```
　　int fieldCount = sqlite3_column_count(...);

　　while (sqlite3_step(...) <> EOF)

　　{

　　　　 for (int i = 0; i < fieldCount; ++i)

　　　　 {

　　　　　　 int v = sqlite3_column_int(...,i);

　　　　 }

　　 }
```
5). sqlite3_finalize
6). sqlite3_close


# 特殊情况

07:29 看一下 sqlite 创建表的语句执行多次是什么效果。 A:不能创建两遍，准备 sql 的时候会出错。
08:01 看一下 sqlite 主键已存在时，插入同主键记录。 A:不能插入成功，没出错。
貌似插入和更新成功返回的是 101，插入失败是 19，只要执行不出错，没更新到也是 101



