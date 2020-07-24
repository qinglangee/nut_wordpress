# python 错误处理

[Python 异常处理](https://www.runoob.com/python/python-exceptions.html)  
## 异常捕捉

所有异常

    try:
        正常的操作
       ......................
    except:
        发生异常，执行这块代码
       ......................
    else:
        如果没有异常执行这块代码

指定类型的异常

    try:
        正常的操作
       ......................
    except(Exception1[, Exception2[,...ExceptionN]]]):
       发生以上多个异常中的一个，执行这块代码
       ......................
    else:
        如果没有异常执行这块代码

try-finally 语句
try-finally 语句无论是否发生异常都将执行最后的代码。

    try:
    <语句>
    finally:
    <语句>    #退出try时总会执行
    raise
实例
```
    #!/usr/bin/python
    # -*- coding: UTF-8 -*-

    try:
        fh = open("testfile", "w")
        fh.write("这是一个测试文件，用于测试异常!!")
    finally:
        print "Error: 没有找到文件或读取文件失败"
```









