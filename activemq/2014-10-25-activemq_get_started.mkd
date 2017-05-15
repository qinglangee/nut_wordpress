# activemq 安装 and 使用入门

*activemq 已经有下一代产品: apollo*

软硬件要求就不说了, 看下面引用文章相关. windows的安装也不说了, 服务器大多用linux吧.

下载, 这里下载一个5.9.1版本的. 它就是个java程序, 解压就可以用了

	> wget http://mirrors.hust.edu.cn/apache/activemq/5.9.1/apache-activemq-5.9.1-bin.tar.gz
	> tar zxvf activemq-x.x.x.tar.gz
	> cd [activemq_install_dir]/bin
	> chmod 755 activemq
启动, Unix版本

	> bin/activemq start
	或者
	> nohup bin/activemq start > /tmp/smlog  2>&1 &;
broker 默认端口使用 61616  
web 控制台页面地址[http://localhost:8161/admin](http://localhost:8161/admin),   默认用户名/密码  admin/admin.   

停止服务, stop 或者 kill pid.  

	> bin/activemq stop

## activemq 配置
没有配置文件时, 用默认配置, 服务会自动寻找下面位置的配置文件. 分别对应全局的和用户的

	/etc/default/activemq 
	/home/lifeix/.activemqrc
可以用下面的命令创建一个配置文件 

	bin/activemq setup [ /etc/default/activemq | /home/lifeix/.activemqrc ]
开启控制台登录验证,	`${ACTIVEMQ_HOME}/conf/jetty.xml `, 属性 authenticate 值改为true

	<property name="authenticate" value="false" />
文件 `${ACTIVEMQ_HOME}/conf/jetty-realm.properties` 里面配置了用户信息.

### 配置持久化存储消息

TODO


refs:  

[ActiveMq Version 5 Getting Started][1]  


[1]: http://activemq.apache.org/version-5-getting-started.html
