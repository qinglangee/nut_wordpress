# mysql 函数

*字符串长度*  [Mysql 字符串函数大全][1]
length：返回字符串所占的字节数
char_length：返回字符串所占的字符数

	select LENGTH(fname)  , char_length(lname) from t ;
*连接字符串*
CONCAT(str1,str2,...)

	SELECT CONCAT('My', 'S', 'QL');
*子字符串*  [SQL 中的 substring 函数][3]  
substr(string string,num start,num length);
string为字符串； start为起始位置,start是从1开始的； length为长度。

	select userid,resume_id,substr(resume_id,2,3) from download_profile
*字符串位置*
INSTR(str,substr)  [13.5 String Functions][4]  
返回substr在 str 中第一次出现的位置，索引从 1 开始。 This is the same as the two-argument form of LOCATE(), except that the order of the arguments is reversed. 

	mysql> SELECT INSTR('foobarbar', 'bar');
	        -> 4
	mysql> SELECT INSTR('xbar', 'foobar');
	        -> 0
## 分组数据
取分组里的最大值 [MySQL Max()函数][2]

	select gid, max(update_time), max(userId) uid from resume_profile  group by gid order by gid desc, uid desc;

refs:
[Mysql 字符串函数大全][1]  
[MySQL Max()函数][2]  




[1]: http://dev.mysql.com/doc/refman/5.0/en/string-functions.html
[2]: http://www.yiibai.com/mysql/mysql_max_function.html
[3]: https://www.1keydata.com/cn/sql/sql-substring.php
[4]: http://dev.mysql.com/doc/refman/5.7/en/string-functions.html#function_instr