# chkconfig 相关内容



服务不支持 chkconfig　的解决方法

这两天一直在研究系统服务，在chkconfig --add  servername的时候老是提示服务不支持 chkconfig　经过查找，解决办法如下。

## 示例，auto_run的前三行如下：

    #!/bin/sh
    #chkconfig: 2345 80 90
    #description:auto_run

* 第一行，告诉系统使用的shell,所以的shell脚本都是这样。
* 第 二行，chkconfig后面有三个参数2345,80和90告诉chkconfig程序，需要在rc2.d~rc5.d目录下，创建名字为 `S80auto_run` 的文件连接，连接到`/etc/rc.d/init.d`目录下的的`auto_run`脚本。
第一个字符是S，系统在启动的时候，运行脚 本`auto_run`，就会添加一个start参数，告诉脚本，现在是启动模式。同时在rc0.d和rc6.d目录下，创建名字为`K90auto_run`的 文件连接，第一个字符为K，个系统在关闭系统的时候，会运行`auto_run`，添加一个stop，告诉脚本，现在是关闭模式。
* 第三行是描述， 不同的服务填个不同的名字， 生成的文件就不同


注意上面的三行是中，第二，第三行是必须的，否则在运行chkconfig --add auto_run时，会报错。
## 常见的错误
>“服务不支持 chkconfig”：
        
请注意检查脚本的前面，是否有完整的两行：

    #chkconfig: 2345 80 90
    #description:auto_run

在脚本前面这两行是不能少的，否则不能chkconfig命令会报错误。
如果运行chkconfig老是报错，如果脚本没有问题，我建议，直接在rc0.d~rc6.d下面创建到脚本的文件连接来解决，原理都是一样的。 

	#ln -s /etc/init.d/httpd /etc/rc.d/rc3.d/S61httpd
	#ln -s /etc/init.d/httpd /etc/rc.d/rc4.d/S61httpd
	#ln -s /etc/init.d/httpd /etc/rc.d/rc5.d/S61httpd


copied from [服务不支持 chkconfig　的解决方法 ](http://blog.csdn.net/blueman2012/article/details/6706572) 