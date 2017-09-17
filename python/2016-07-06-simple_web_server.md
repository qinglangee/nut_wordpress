# python 启动简单的 web server

利用Python自带的包可以建立简单的web服务器。在DOS里cd到准备做服务器根目录的路径下，输入命令：

    python -m Web服务器模块 [端口号，默认8000]

例如：

    python -m SimpleHTTPServer 8080

然后就可以在浏览器中输入

    http://localhost:端口号/路径

来访问服务器资源。 
例如：

    http://localhost:8080/index.htm（当然index.htm文件得自己创建）

其他机器也可以通过服务器的IP地址来访问。


这里的“Web服务器模块”有如下三种：

    BaseHTTPServer: 提供基本的Web服务和处理器类，分别是HTTPServer和BaseHTTPRequestHandler。
    SimpleHTTPServer: 包含执行GET和HEAD请求的SimpleHTTPRequestHandler类。
    CGIHTTPServer: 包含处理POST请求和执行CGIHTTPRequestHandler类。

## CGIHTTPServer
1 进入某个你想创建为服务器的文件夹，假如文件夹名为www。从cmd进入www文件夹，运行python -m CGIHTTPServer，默认端口是8000

	python -m CGIHTTPServer 8888
2 进入www文件夹，新建一个cgi-bin 或者 htbin 的文件夹，用来存放.py文件，原因看官方文件：http://docs.python.org/2/library/cgihttpserver.html?highlight=cgihttpserver#CGIHTTPServer

3  在cgi-bin文件中新建form.py文件 

	#! /usr/bin/env python
	# -*- coding: utf-8 -*-

	import cgi

	header = 'Content-Type: text/html\n\n'

	html = '<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /></head><h3>接受处理表单数据\n</h3>'
	#打印返回的内容
	print header
	print html
	# 接受表单提交的数据
	form = cgi.FieldStorage()

	print '接收表达get的数据 ：',form

	print '<p />'

	# 解析处理提交的数据
	content = form['text'].value

	formhtml = '''
	<label for="">you say:</label><input type="text" value="%s">
	'''

	print formhtml % (content)
	print '</html>'



- 报错  OSError: [Errno 13] Permission denied
	*xxx.py 文件要加上可执行权限* 
- 报错  OSError: [Errno 8] Exec format error
	在程序第一行加入：　`#! /usr/bin/env python`　　如果是python3运行的话把 python 换成 python3


4  访问 http://localhost:8888/cgi-bin/form.py?text=test  进行测试

## 控制其它程序
如果要通过server控制其它程序，需要有相关的权限．用root帐号启动的话，会被赋于nobody的权限．　　
可以用一个非root用户启动被控制程序，再用相同用户启动server.
`su - seimiagent -c "cd /srv/seimi_ctrl_server && nohup python -m CGIHTTPServer 8001 &"`  指定seimiagent用户启动　CGIHTTPServer.

refs:  
[用Python建立最简单的web服务器 ](http://www.cnblogs.com/xuxn/archive/2011/02/14/build-simple-web-server-with-python.html)  
[CGIHTTPServer](https://docs.python.org/2/library/cgihttpserver.html)  
[python自带CGIHTTPServer服务器与htm进行CGI交互](http://blog.csdn.net/dijason/article/details/8256372)  
[python 出现OSError: Errno 8 Exec format error的原因](http://www.cnblogs.com/dreamtecher/p/5096488.html)  