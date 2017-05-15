# python 处理 json

使用简单的json.dumps方法对简单数据类型进行编码，例如：
	
	import json
	 
	obj = [[1,2,3],123,123.123,'abc',{'key1':(1,2,3),'key2':(4,5,6)}]
	encodedjson = json.dumps(obj)
	print repr(obj)
	print encodedjson
输出：

>[[1, 2, 3], 123, 123.123, 'abc', {'key2': (4, 5, 6), 'key1': (1, 2, 3)}]
>[[1, 2, 3], 123, 123.123, "abc", {"key2": [4, 5, 6], "key1": [1, 2, 3]}]

通过输出的结果可以看出，简单类型通过encode之后跟其原始的repr()输出结果非常相似，但是有些数据类型进行了改变，例如上例中的元组则转换为了列表。在json的编码过程中，会存在从python原始类型向json类型的转化过程，具体的转化对照如下：

Python              JSON
dict                Object
list, tuple         array
str, unicode        string
int, long, float    number
Ture                true
False               false
None                null

json.dumps()方法返回了一个str对象encodedjson，我们接下来在对encodedjson进行decode，得到原始数据，需要使用的json.loads()函数：
	
	decodejson = json.loads(encodedjson)
	print type(decodejson)
	print decodejson[4]['key1']
	print decodejson

输出：

><type 'list'>
>[1, 2, 3]

>[[1, 2, 3], 123, 123.123, u'abc', {u'key2': [4, 5, 6], u'key1': [1, 2, 3]}]


json.dumps方法提供了很多好用的参数可供选择，比较常用的有sort_keys（对dict对象进行排序，我们知道默认dict是无序存放的），separators，indent等参数。

	data1 = {'b':789,'c':456,'a':123}
	data2 = {'a':123,'b':789,'c':456}
	d1 = json.dumps(data1,sort_keys=True)

	d1 = json.dumps(data1,sort_keys=True,indent=4)
	print d1



refs:  
[Json概述以及python对json的相关操作](http://www.cnblogs.com/coser/archive/2011/12/14/2287739.html)  
[json 官方文档](http://docs.python.org/library/json.html#module-json)  