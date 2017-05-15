# nginx配置 / 的区别

nginx 的proxy_pass 基本设置问题

    曾在网上看到一些问题，比如 nginx 的proxy_pass后面的地址加“/”与不加“/”有区别。

   参看nginx英文文档后，发现：

If it is necessary to transmit URI in the unprocessed form then directive proxy_pass should be used without URI part:

location  /some/path/ {
  proxy_pass   http://127.0.0.1;
}

大概意思就是说，如果你不想nginx对你的URI请求有任何形式的修改，那么，proxy_pass的配置中就不应该有任何URI部分。

举个例子，nginx服务器IP为10.0.0.20，它的配置不含URI：

location /first/second/ {
        proxy_pass http://10.0.0.30:90;
}
那么，

原：     http://10.0.0.20/first/second/test.html
转：http://10.0.0.30:90/first/second/test.html


 割一下，如果配置成含URI：
location /first/second/ {
proxy_pass http://10.0.0.30:90/myuri;
}
那么，

原： http://10.0.0.20/first/second/test.html
转：http://10.0.0.30:90/myuri/test.html
简单地说，配置了URI之后，跳转行为可能会令你感到莫名其妙，要有充分的思想准备。


还要注意， /first/second/ 最后的斜线，有与没有的区别

下面四种情况分别用http://192.168.1.4/proxy/test.html 进行访问。

第一种：

    location  /proxy/ {
              proxy_pass http://127.0.0.1:81/;
    }
会被代理到http://127.0.0.1:81/test.html 这个url
第二种：(相对于第一种，最后少一个 /)

    location  /proxy/ {
              proxy_pass http://127.0.0.1:81;
    }
会被代理到http://127.0.0.1:81/proxy/test.html 这个url
第三种：

    location  /proxy/ {
              proxy_pass http://127.0.0.1:81/ftlynx/;
    }

会被代理到http://127.0.0.1:81/ftlynx/test.html 这个url。
第四种情况：(相对于第三种，最后少一个 / )：

    location  /proxy/ {
              proxy_pass http://127.0.0.1:81/ftlynx;
    }

会被代理到http://127.0.0.1:81/ftlynxtest.html 这个url

[原文：nginx proxy_pass后的url加不加/的区别][2]

## location 配置中 root 与 alias 的区别

如下配置  www.abc.com/static/aa.js 就会访问 /srv/web/static/aa.js文件

	location /static {
		root  /srv/web/
	}
如下配置  www.abc.com/static/aa.js 也会访问 /srv/web/static/aa.js文件

	location /static {
		alias  /srv/web/static
	}


参考:
[nginx 的proxy_pass 基本设置问题][1]  

[1]: http://hi.baidu.com/dudangyimian/item/14586c34c2af89f3e7bb7a8e
[2]: http://ftlynx.blog.51cto.com/2833447/839607
