# ssh 共享连接

修改ssh配置

按照下面的内容修改这个文件vim ~/.ssh/config

	ControlMaster auto 
	##ControlPath /tmp/%r@%h:%p 
	ControlPath /tmp/git@github.com:22 
	ControlPersist yes
一些注解

    ControlMaster auto 可以使多个ssh会话共享一个已经存在的连接，如果没有，则自动创建一个连接。
    ControlPath /tmp/%r@%h:%p 可以指定想要共享的连接。%r代表远程登录用户名，一般都为git，%h表示目标主机，%p表示端口。
    ControlPersist yes 则可以让共享的连接持有处于连接状态。

常用的ControlPath

下面包含开源中国，github，gitcafe等代码托管。

	ControlPath /tmp/git@git.oschina.net:22 
	ControlPath /tmp/git@github.com:22 
	ControlPath /tmp/git@gitcafe.com:22

快来试一试吧，是不是提高了5倍！

注：由于网络的情况，结果可能略有不同。已经很快的但没有感觉改善的同学，可以继续读下去。
还能更快

还有一个能提高50倍的方法，不过对于一般开发者不是很常用，如需了解可以参考[Speed Up Git (5x to 50x)][1]  


refs:  
[人生苦短，让你的Git飞起来吧][2]  
[人生苦短，让你的Git飞起来吧][3]  



[1]: http://interrobeng.com/2013/08/25/speed-up-git-5x-to-50x/
[2]: http://droidyue.com/blog/2014/10/15/speed-up-your-git/
[3]: http://www.udpwork.com/item/13393.html