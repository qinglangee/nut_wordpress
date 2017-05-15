# python 按行读取文件


##　1. 最基本的读文件方法：

 
	file = open("sample.txt")
	 
	while 1:
	    line = file.readline()
	    if not line:
	        break
	    pass # do something

　　一行一行得从文件读数据，显然比较慢；不过很省内存。

　　在我的机器上读10M的sample.txt文件，每秒大约读32000行

##　2. 用fileinput模块
 
	import fileinput
	 
	for line in fileinput.input("sample.txt"):
	    pass

　　写法简单一些，不过测试以后发现每秒只能读13000行数据，效率比上一种方法慢了两倍多……

##　3. 带缓存的文件读取
 
	file = open("sample.txt")
	 
	while 1:
	    lines = file.readlines(100000)
	    if not lines:
	        break
	    for line in lines:
	        pass # do something

　　这个方法真的更好吗？事实证明，用同样的数据测试，它每秒可以读96900行数据！效率是第一种方法的3倍，第二种方法的7倍！

————————————————————————————————————————————————————————————

##　在Python 2.2以后，我们可以直接对一个file对象使用for循环读每行数据：
 
	file = open("sample.txt")
	 
	for line in file:
	    pass # do something

## 而在Python 2.1里，你只能用xreadlines迭代器来实现：
 
	file = open("sample.txt")
	 
	for line in file.xreadlines():
	    pass # do something


refs:  
[Python按行读文件](http://www.cnblogs.com/xuxn/archive/2011/07/27/read-a-file-with-python.html)  