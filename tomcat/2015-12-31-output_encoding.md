# tomcat 中文输出乱码问题
tomcat中打印中文日志全是问号 ??????
`System.getProperty("file.encoding")`  输出值是  ANSI_X3.4-1968

解决的方法有：

1 打开catalina.sh，在代码的第一行即set CATALINA_OPTS之前，增加一行：

    set JAVA_OPTS=%JAVA_OPTS%  -Dfile.encoding=UTF-8
2 修改启动用户的环境编码, 在 tomcat 的 service 启动脚本中

	export LC_ALL='en_US.UTF-8'


[Linux下Java写文件ANSI_X3.4-1968的问题][1]  

>仔细想想，这个问题和我之前遇到的Git不能提交的问题有点像。因为更改了apache的默认运行用户，导致git用户无法读取自己的.config文件，所以提交不了。

refs:  
[Linux下Java写文件ANSI_X3.4-1968的问题][1]  
[UnicodeEncodeError when saving ImageField containing non-ASCII characters in Django admin][2]  
[解决Logback生成的日志文件不能显示中文的问题 ][3]  


[1]: http://www.cnblogs.com/trying/archive/2012/12/07/2863849.html
[2]: http://stackoverflow.com/questions/4398540/unicodeencodeerror-when-saving-imagefield-containing-non-ascii-characters-in-dja
[3]: blog.csdn.net/mydeman/article/details/6177363