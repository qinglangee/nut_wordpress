# python 正则表达式

# ====================================================
链接原文待完善

# re.match函数

re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none
	import re
	print(re.match('www', 'www.runoob.com').span())  # 在起始位置匹配
	print(re.match('com', 'www.runoob.com'))         # 不在起始位置匹配


refs:  
[python 正则表达式](http://www.runoob.com/python/python-reg-expressions.html)  
[python 正则匹配中文](http://www.blogjava.net/Skynet/archive/2009/05/02/268628.html)  