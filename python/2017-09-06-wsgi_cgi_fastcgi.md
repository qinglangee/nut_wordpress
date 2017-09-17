# 各种GI的关系

## WSGI 
The Web Server Gateway Interface
WSGI是python关于web服务器的一个标准，是python语言实现的web框架需要遵守的一套标准．
WSGI 再通过一些库(如flup)提供的接口与各种CGI进行交互．
## CGI
Common Gateway Interface
CGI是web服务器与程序语言之间的通讯接口．像是Apache,Nginx这种通用web服务器与不同程序语言交互的接口．
## FASTCGI
Fast Common Gateway Interface
FASTCGI 是CGI的改良版本，CGI每次都是重启一个进程处理请求，FASTCGI则是有常驻内存的进程管理机制．
## SCGI
Simple Common Gateway Interface
SCGI则是与FASTCGI类似，但是简单版本．