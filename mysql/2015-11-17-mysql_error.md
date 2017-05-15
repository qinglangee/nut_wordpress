# mysql 错误


##  can not be represented as java.sql.Timestamp 

使用hibernate开发程序的时候，有的时间字段没有必要填写，但是，以后hibernate查询的时候会报出
“java.sql.SQLException: Value '0000-00-00' can not be represented as java.sql.Timestamp”
的错误， 这是因为hibernate认为这个不是一个有效的时间字串。
而有效的日期格式为“ 0001-01-01   00:00:00.0 ”

所以， 我们在jdbc连接出改成
	`"jdbc:mysql://localhost:3306/test?useUnicode=true&amp;characterEncoding=UTF8&amp;zeroDateTimeBehavior=convertToNull"`
或者
	`"jdbc:mysql://localhost:3306/test?useUnicode=true&amp;characterEncoding=UTF8&amp;zeroDateTimeBehavior=round   0001-01-01   00:00:00.0 "`
就解决这个问题了。

[can not be represented as java.sql.Timestamp](http://blog.csdn.net/educast/article/details/45582497)  
[can not be represented as java.sql.Timestamp](http://aaagu1234.blog.163.com/blog/static/40093715201091313642829/)  