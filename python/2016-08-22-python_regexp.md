# python 正则表达式
[python 正则表达式](http://www.runoob.com/python/python-reg-expressions.html)  

# ====================================================
看第一个链接
看第一个链接
看第一个链接

# re.match函数

re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none

    re.match(pattern, string, flags=0)

flags    标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。
正则表达式修饰符 - 可选标志

正则表达式可以包含一些可选标志修饰符来控制匹配的模式。修饰符被指定为一个可选的标志。多个标志可以通过按位 OR(|) 它们来指定。如 re.I | re.M 被设置成 I 和 M 标志：
修饰符 描述
re.I    使匹配对大小写不敏感
re.L    做本地化识别（locale-aware）匹配
re.M    多行匹配，影响 ^ 和 $
re.S    使 . 匹配包括换行在内的所有字符
re.U    根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.
re.X    该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解

	import re
	print(re.match('www', 'www.runoob.com').span())  # 在起始位置匹配 用span()
	print(re.match('com', 'www.runoob.com'))         # 不在起始位置匹配, 返回 None


group(num=0)    匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。
groups()    返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。

```
#!/usr/bin/python
import re
 
line = "Cats are smarter than dogs";
 
searchObj = re.search( r'(.*) are (.*?) .*', line, re.M|re.I)
 
if searchObj:
   print "searchObj.group() : ", searchObj.group()
   print "searchObj.group(1) : ", searchObj.group(1)
   print "searchObj.group(2) : ", searchObj.group(2)
else:
   print "Nothing found!!"
```

# re.search 
re.search 扫描整个字符串并返回第一个成功的匹配。 
`re.search(pattern, string, flags=0)`

refs:  
[python 正则表达式](http://www.runoob.com/python/python-reg-expressions.html)  
[python 正则匹配中文](http://www.blogjava.net/Skynet/archive/2009/05/02/268628.html)  