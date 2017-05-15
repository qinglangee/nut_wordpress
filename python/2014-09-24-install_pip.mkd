# 安装包管理器pip



装python的包可以自己下来直接装，也可以通过pip来通过网络安装。  

[pip 最新版安装](http://www.pip-installer.org/en/latest/installing.html)

上面的链接包含了详细的过程。我这里只记录几个简要的命令给自己以后查用。  

1.安装   

	wget  https://bootstrap.pypa.io/get-pip.py
	sudo python get-pip.py

2.运行  
可以通过pip help来查看帮助。简单用的话只要pip search和pip install就好了。  


## 用pip 安装包

	pip install pyquery
有些不好安装的包，例如 `lxml` 可以在一个[非官方二进制包提供网站][1] 上下载包直接安装


refs:  
[【python】python安装lxml报错【2】](http://www.cnblogs.com/silenceli/p/4140077.html)  
[lxml Installation Failure](https://pytools.codeplex.com/workitem/1520)  
[lxml-install-on-windows-7-using-pip-and-python-2-7](http://stackoverflow.com/questions/20460890/lxml-install-on-windows-7-using-pip-and-python-2-7)  



[1]: http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml
