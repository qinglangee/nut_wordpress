# python string 处理函数


项目中有个功能要求将字符串第一个字母改为大写，查了文档及搜索引擎，没找到，自己写了一个，非常简单
```
def upperFirstWord(inStr):
    return "%s" % (inStr[:1].upper() + inStr[1:])
```
 

# 顺便温习一下下面这几个同类型函数：

`capitalize()` 首字母大写，其余全部小写 
`upper()` 全转换成大写
`lower()` 全转换成小写
`title()`  标题首字大写，如"i love python".title()  "I Love Python"

```
a = "i love python"
b = "MARK"

print a.capitalize()  # I love python
print a.upper()       # I LOVE PYTHON
print b.lower()       # mark
print a.title()       # I Love Python
```

# 字符串替换 

	a = 'hello word'  # 我把a字符串里的word替换为python

	1用字符串本身的replace方法
	a.replace('word','python')

	2用正则表达式来完成替换:
	import re
	strinfo = re.compile('word')
	b = strinfo.sub('python',a)
	print b
	输出的结果也是hello python
# 字符串包含

	if("aa" in "aabc"):
		print "aa in aabc"  # true false
	index = "abcdaabc".find("aa")  # index == 4
# 字符串去两头空格

	str = "  aa  "
	str.strip()
	str.lstrip()  # 去左边空格
	str.rstrip()  # 去右边空格
# 字符串截取
	
	aa = "123456"
	a1 = aa[:-1]  # 12345
	a2 = aa[1:]  # 23456
	a3 = aa[1:3]  # 23
	a4 = aa[2:4]  # 34
	a5 = aa[0:3]  # 123
	a6 = aa[0:]  # 123456
	a6 = aa[0:12]  # 123456
# 字符串开头结尾

	content.startswith("ilove")
	content.endswith("ilove")
    str.startswith(str, beg=0,end=len(string));
    str.startswith( 'is', 2, 4 )

# 字符串与二制数据转换

python3中

	aa = "杨雪".encode('utf-8')   # 【默认格式utf-8】     转化后结果：b'\xe6\x9d\xa8\xe9\x9b\xaa'
	print(aa)
	bb = b'\xe6\x9d\xa8\xe9\x9b\xaa'.decode('utf-8')   # 【默认格式utf-8】  转化后结果为：杨雪
	print(bb)    
	cc = "杨雪".encode()   # 【默认格式utf-8】     转化后结果：b'\xe6\x9d\xa8\xe9\x9b\xaa'
	print(cc)

# 字符串格式化

	print('I am %s' % 'zhangsan')  # 一个参数
	print('I am %s, my age is %d' % ('bob', 25))  # 多个参数

# 字符串连接


	list = ["a","b","c"]
	"-".join()   # 结果是  a-b-c

# 字符串与数字互转

## 字符串与整数互转

	numStr = '123'
	aa = int(numStr)
	bb = '%d' % aa

	import random
	mm = str(random.randint(0,9))

	print(numStr + bb)
	print(aa + 3)






refs:  
[python 大小写转换函数](http://www.cnblogs.com/bjdxy/archive/2012/11/22/2783107.html)  