# mysql 存储过程

## 创建存储过程
命令行创建存储过程

	mysql > DELIMITER $$ 
	mysql > CREATE PROCEDURE demo_in_parameter(IN p_in int)  
	-> BEGIN   
	-> SELECT p_in;   
	-> SET p_in=2;   
	-> SELECT p_in;   
	-> END;   
	-> $$ 
	mysql > DELIMITER ; 
这里需要注意的是DELIMITER $$ 和DELIMITER ;两句，DELIMITER是分割符的意思，因为MySQL默认以";"为分隔符，如果我们没有声明分割符，那么编译器会把存储过程当成SQL语句进行处理，则存储过程的编译过程会报错，所以要事先用DELIMITER关键字申明当前段分隔符，这样MySQL才会将";"当做存储过程中的代码，不会执行这些代码，用完了之后要把分隔符还原。

用法示例

	DROP PROCEDURE IF EXISTS sqtzhch.delete_profile_by_file_id;
	CREATE PROCEDURE sqtzhch.`delete_profile_by_file_id`(IN p_fileId int, IN p_upload_type int)
	BEGIN   

	  -- switch 的 mysql 写法
	  CASE p_upload_type
	  WHEN 1 THEN 
	    update web_upload_profile_resume_info set status=0 where id=p_fileId;
	  ELSE 
	    update web_upload_resume_info set status=0 where id=p_fileId;
	  END CASE;

	  
	  delete from resume_certificate where userid in (select userid from resume_profile where fileId = p_fileId AND upload_type=p_upload_type);
	  
	  delete from resume_parse_error_file where file_id=p_fileId AND upload_type=p_upload_type;
	END;

## 执行存储过程

	demo_in_parameter(123); 

## 删除存储过程

	drop procedure your_proc_name;
## 查询存储过程

方法一：（直接查询）

	select `specific_name` from mysql.proc where db = 'your_db_name' and `type` = 'procedure'

方法二：（查看数据库里所有存储过程+内容）

	show procedure status;

方法三：（查看当前数据库里存储过程列表）

	select specific_name from mysql.proc ;

方法四：(查看某一个存储过程的具体内容)

	select body from mysql.proc where specific_name = 'your_proc_name';

查看存储过程或函数的创建代码 ：

	show create procedure your_proc_name;
	show create function your_func_name;





refs:  
[MySQL存储过程](http://www.cnblogs.com/exmyth/p/3303470.html)  
[mysql存储过程查看，修改，删除，创建方法](http://www.111cn.net/database/mysql/35817.htm)  
[MySql存储过程—5、逻辑判断，条件控制](http://www.2cto.com/database/201208/149282.html)  