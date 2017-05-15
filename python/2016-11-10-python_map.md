# map 相关内容



## 如何判断字典中是否存在某个key，一般有两种通用做法，下面为大家来分别讲解一下：

第一种方法：使用自带函数实现。 在python的字典的属性方法里面有一个has_key()方法，这个方法使用起来非常简单。
	
	d = {'name':{},'age':{},'sex':{}}  #生成一个字典
	print d.has_key('name')  #打印返回值   #打印返回值
第二种方法：使用in方法

	d = {'name':{},'age':{},'sex':{}}   #生成一个字典
	print 'name' in d.keys()  #打印返回值，其中d.keys()是列出字典所有的key  #结果返回True
上面两种方式，我更推荐使用第二种，因为has_key()是python2.2之前的方法，而且使用in的方法会更快一些。
最后告诉大家一点：除了使用in还可以使用not in，判定这个key不存在哦~


refs:  
[判断python字典中key是否存在的两种方法](http://www.pythontab.com/html/2012/pythonjichu_1227/67.html)  