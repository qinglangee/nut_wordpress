# python 执行系统命令

## 比较新的方法

获取标准输出

	import traceback
	import subprocess

	try:
	    app = ['/usr/bin/ls', '/tmp'] #call the java programe
	    proc = subprocess.Popen(app,stdout=subprocess.PIPE)      #redirect the python out
	    output = proc.stdout.read()
	    print "output is : " +  output
	except Exception as e:
	    exstr = traceback.format_exc()
	    print exstr

    # 放在函数中调用
	import traceback
	import subprocess

	def getkeyword(puretext):
	    try:
	        app = ['/usr/bin/lssdd', '/tmp'] #call the java programe
	        proc = subprocess.Popen(app,stdout=subprocess.PIPE)      #redirect the python out
	        return proc.stdout.read()
	    except Exception as e:
	        exstr = traceback.format_exc()
	        print exstr
	        return "ERROR"

	print getkeyword('123')



## 以前的方法
 Python中执行系统命令常见方法有两种：


两者均需 import os

(1) os.system

* 仅仅在一个子终端运行系统命令，而不能获取命令执行后的返回信息

system(command) -> exit_status
Execute the command (a string) in a subshell.

* 如果再命令行下执行，结果直接打印出来

执行
1	>>> os.system('ls')
2	04101419778.CHM   bash      document    media      py-django   video
3	11.wmv            books     downloads   Pictures  python
4	all-20061022      Desktop   Examples    project    tools

(2) os.popen

* 该方法不但执行命令还返回执行后的输出信息对象

popen(command [, mode='r' [, bufsize]]) -> pipe
Open a pipe to/from a command returning a file object.

	# execute command, and return the output  
	def execCmd(cmd):  
	    r = os.popen(cmd)  
	    text = r.read()  
	    r.close()  
	    return text  
	text = execCmd('ls')   # text 是 执行 ls 命令后的输出





refs:  
[Python执行系统命令的方法](http://www.cnblogs.com/xuxm2007/archive/2011/01/17/1937220.html)  
[python 的 subprocess模块用法 popen ](http://blog.csdn.net/g457499940/article/details/17068277)  