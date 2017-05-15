# windows 下安装使用 python mysql 模块

## 下载
[官网下载](https://pypi.python.org/pypi/MySQL-python/)  

好像很难装的样子，见[某人的经历](http://www.crifan.com/python_install_module_mysql_mysqldb/)  

后来下了个 [oracle 出品的](http://dev.mysql.com/downloads/connector/python/)， 一下子就装好了， 但还不会用， 再看看怎么用吧。

mysqldb 用了一个c模块连接数据库， 效率上比 mysql-connector 要高一些。
在[这篇比较的文章][1]中还提到了一个性能测试的工具 `cProfile` 。




refs:  
[MySQL Python教程（2）](http://www.cnblogs.com/bigbigtree/archive/2013/08/08/3246718.html)  


[1]: http://www.th7.cn/Program/Python/201511/705254.shtml