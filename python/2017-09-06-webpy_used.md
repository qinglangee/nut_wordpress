# 使用web.py搭建简单web服务
web.py自带web服务器，也可以通过cgi,fastcgi与apache,nginx等合作．

## 安装
１．包管理器安装
`sudo pip install web.py`
２．源码安装
到　https://github.com/webpy/webpy/tarball/master　下载最新版本，把web目录copy到程序目录．

## 最小程序
新建 code.py
```
import web
        
urls = (
    '/(.*)', 'hello'
)

class hello:        
    def GET(self, name):
        if not name: 
            name = 'World'
        return 'Hello, ' + name + '!'

if __name__ == "__main__":
    app = web.application(urls, globals())
    app.run()
```
## 启动服务器
`python code.py` 默认端口 8080 , 指定端口使用`python code.py  1234`


## 重定向请求　redirect
web.seeother 和 web.redirect, seeother发送303, 是临时重定向，　redirect 发送301，是永久重定向
```
class SomePage:
    def POST(self):
        # Do some application logic here, and then:
        raise web.seeother('/someotherpage')
```


refs:  
[web.py Tutorial](http://webpy.org/docs/0.3/tutorial)  