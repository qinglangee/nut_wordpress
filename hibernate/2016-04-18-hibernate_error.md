# hibernate 常见错误

## Found shared references to a collection
case 1:

假定,Parent类有一个Set属性，里面放的是Son。如果查询"from Parent",某个Parent哪怕一个Son都没有，那个Set属性不会为null，而是一个空集合。
这时候如果你Parent newP=new Parent();然后BeanUtils.copyPropertis(newP,origP);最后就会报hibernate异常"Found shared references to a collection"。
原因:
BeanUtils.copyPropertis是浅拷贝，导致这两个对象引用的Set是同一个Set,这在hibernate中是不允许的
[hibernate异常"Found shared references to a collection](blog.163.com/cjp1320@126/blog/static/3547436320092411404550/)    

case 2:
同一个查询执行多次

	oldList = downloadProfileService.getDownloadProfile(bean.getResume_id(), 2);
	newList = downloadProfileService.getDownloadProfile(bean.getResume_id(), 2);
## Batch update returned unexpected row count from update [0]; actual row count: 0;  
使用了hibernate的主键生成策略，而在程序中又主动去设置了主键值。
[异常:Batch update returned unexpected row count from update [0]; actual row count: 0;  ](http://daizhenghua.good.blog.163.com/blog/static/105287726201262314754831/)  
[hibernate主键生成策略](http://elliotwhisper.com/batch-update-returned-unexpected-row-count-from-update-0-actual-row-count-0-expected-1.htm)  

## More than one row with the given identifier was found
在一对一 @OneToOne 关联中， 主表所用的关联字段在从表中不是唯一索引，从表中产生了多条记录。  
或者 @ManyToOne 关系也有可能产生，没有试验过。
## Batch update returned unexpected row count from update [0]; actual row count: 0; expected: 1
不注意的话，还真的有点无所适从，Batch update returned unexpected row count from update [0]; actual row count: 0; expected: 1这个异常是由于主键设置为自增长，而在我们插入记录的时候设置了ID的值导致的。
[网络收集](http://blog.csdn.net/ssyan/article/details/7471343)  

## object references an unsaved transient instance - save the transient instance before flushing
这主要是在ManyToOne级联操作时遇到， OneToOne时也会有,比如new了一个新对象，在未保存之前将它保存进了一个新new的对象（也即不是持久态）。

解决办法 1 是在新对象中给关联字段设置上正确的值，保存时会自动生成新记录。
解决办法 2 是在保存或更新之前把这个对象查出来（这样就是一个持久态）。
解决办法 3 是将many-to-one的级联设为: cascade="save-update,persist" 

## Write operations are not allowed in read-only mode
只读事务中不允许进行写操作

原因一， Open Session In View， 默认开的事务是只读的
原因二， service 没有被 transactionManager 管理到， 默认开了个只读事务。 比如 切面是 com.aa.service  , 但 service 在 com.bb.service 中