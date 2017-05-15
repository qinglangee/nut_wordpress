# mongodb 慢查询

## 开启慢查询记录
有两种方式可以控制 Profiling  的开关和级别，第一种是直接在启动参数里直接进行设置。 启动MongoDB时加上–profile=级别  即可。 
也可以在客户端调用 db.setProfilingLevel(级别)  命令来实时配置，Profiler  信息保存在 system.profile 中。我们可以通过`db.getProfilingLevel()`命令来获取当前的Profile级别，类似如下操作 

	db.setProfilingLevel(2);  
	db.setProfilingLevel(2, 20);  
	db.getProfilingLevel();
	db.getProfilingStatus();

上面profile的级别可以取0，1，2  三个值，他们表示的意义如下： 

- 0 –  不开启 
- 1 –  记录慢命令 (默认为>100ms)  
- 2 –  记录所有命令  

慢命令的时间设置方法和级别一样有两种，一种是通过添加–slowms 启动参数配置。第二种是调用db.setProfilingLevel时加上第二个参数： 

	db.setProfilingLevel( 1 , 10 ); 

## 查询 Profiling  记录 
直接查看system.profile表, 列出执行时间长于某一限度(5ms)的 Profile  记录： 

	db.system.profile.find( { millis : { $gt : 5 } } ) 
查看最新的 Profile  记录： 

	db.system.profile.find().sort({$natural:-1}).limit(1) 

*MongoDB Shell  还提供了一个比较简洁的命令 show profile，可列出最近5 条执行时间超过 1ms 的 Profile 记录。*

## MongoDB 查询优化
如果nscanned(扫描的记录数)远大于nreturned(返回结果的记录数)的话，那么我们就要考虑通过加索引来优化记录定位了。

reslen 如果过大，那么说明我们返回的结果集太大了，这时请查看find函数的第二个参数是否只写上了你需要的属性名。(类似 于MySQL中不要总是select *)

对于创建索引的建议是：如果很少读，那么尽量不要添加索引，因为索引越多，写操作会越慢。如果读量很大，那么创建索引还是比较划算的。(和RDBMS一样，貌似是废话 -_-!!)


参考:
[Mongodb profile（慢查询日志）][1]  
[mongodb慢查询记录（耗时查询的日志记录）][2]  


[1]: http://blog.sina.com.cn/s/blog_7af230cd01010ggh.html
[2]: http://blog.sina.com.cn/s/blog_5f53615f0101448f.html