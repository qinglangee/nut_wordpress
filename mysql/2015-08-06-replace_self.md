# mysql 用 replace 函数更新自己
今天在工作的过程中碰到一个问题，要把数据库中某个列的所有值中含有"shop.xxxx.net"的字符更换成"www.nowamagic.net"，本来可以写个脚本，把所有的值都取出再用php进行处理，但是那样就效率非常低了，想到看试下能不能直接在MySQL中用SQL语句直接来处理，经过一番搜索，终于找到解决方案，其实最重要的是mysql的replace函数，关于这个函数的介绍，我在MySQL手册中是没看懂，不过能实现我想要的功能就行。


下面就是对这个函数的简要介绍以及范例。

比如你要将 表 tb1里面的 f1字段的abc替换为def：

	UPDATE tb1 SET f1=REPLACE(f1, 'abc', 'def');
	REPLACE(str,from_str,to_str)

在字符串 str 中所有出现的字符串 from_str 均被 to_str替换，然后返回这个字符串：

	mysql>   SELECT   REPLACE('www.mysql.com',   'w',   'Ww');
	->   'WwWwWw.mysql.com'

这个函数是多字节安全的。

示例：

	UPDATE  `dede_addonarticle`  SET body =  REPLACE ( body,'</td>'," );
	UPDATE  `dede_addonarticle`  SET body =  REPLACE ( body,'</tr>'," );
	UPDATE  `dede_addonarticle`  SET body =  REPLACE ( body,'<tr>'," );
	UPDATE  `dede_archives`  SET title=  REPLACE ( title,'简明现代魔法 – '," );
	UPDATE  `dede_addonarticle`  SET body =  REPLACE ( body,'../../../../../../','http://special.dayoo.com/meal/' );
mysql replace

用法

1. replace intoreplace into table (id,name) values('1','aa'),('2','bb')

此语句的作用是向表table中插入两条记录。

2. replace(object, search,replace)

把object中出现search的全部替换为replaceselect replace('www.163.com','w','Ww')—>WwW wWw.163.com

例：把表table中的name字段中的 aa替换为bbupdate table set name=replace(name,'aa','bb')
Sql Server 中 text或ntext 字段内容替换

刚开始，Update AA 表 Set xx字段=Replace(xx字段,"要替换的","特定串") ，出现错误：函数 replace 的参数 1 的数据类型 ntext 无效。`Update article set heading=Replace(convert(nvarchar(4000),heading),'<script></script>','')`

	update 表名
	    set text类型字段名=replace(convert(varchar(8000),text类型字段名),'要替换的字符','替换成的值')

varchar和nvarchar类型是支持replace，所以如果你的text/ntext不超过8000/4000可以先转换成前面两种类型再使用replace。

	update 表名
	    set text类型字段名=replace(convert(varchar(8000),text类型字段名),'要替换的字符','替换成的值')
	update 表名
	    set ntext类型字段名=replace(convert(nvarchar(4000),ntext类型字段名),'要替换的字符','替换成的值')

如果text/ntext超过8000/4000,看如下例子：


    declare @pos int
        declare @len int
        declare @str nvarchar(4000)
        declare @des nvarchar(4000)
        declare @count int
       set @des ='<requested_amount+1>'--要替换成的值
     
       set @len=len(@des)
       set @str= '<requested_amount>'--要替换的字符
     
     
       set @count=0--统计次数.
     
     
        WHILE 1=1
       BEGIN
           select @pos=patINDEX('%'+@des+'%',propxmldata) - 1
           from 表名
           where 条件
     
          IF @pos>=0
          begin
               DECLARE @ptrval binary(16)
              SELECT @ptrval = TEXTPTR(字段名)
              from 表名
              where 条件
               UPDATETEXT 表名.字段名 @ptrval @pos @len @str
              set @count=@count+1
           end
          ELSE
             break;
       END
     
       select @count

﻿

注：如需转载本文，请注明出处（原文链接），谢谢。更多精彩内容，请进入简明现代魔法首页。

copyed from:  
[MySQL的replace()函数介绍](http://www.nowamagic.net/database/db_MysqlReplace.php)  