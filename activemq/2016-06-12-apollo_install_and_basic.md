# apollo 安装与使用

## 安装
[下载页面][1] 直接下载 linux 版本解压即可

	tar -zxvf apache-apollo-1.7.1-unix-distro.tar.gz

## 创建一个中间件实例

中间件实例就是一个包含中间件进程需要的所有配置、运行时数据、日志等等内容的目录。 最后与apollo安装目录分开。  
下面命令在  /var/lib/mybroker 目录中创建一个实例。

	cd /var/lib
	${APOLLO_HOME}/bin/apollo create mybroker

你可以启动这个 broker :

    "/var/apollo-brokers/mybroker/bin/apollo-broker" run

也可以把它设置成系统服务，在后台运行:

    sudo ln -s "/var/apollo-brokers/mybroker/bin/apollo-broker-service" /etc/init.d/
    /etc/init.d/apollo-broker-service start
启动后测试一下

	gem install stomp

	cd ${APOLLO_HOME}/examples/stomp/ruby   # 启动一个接收者
	ruby listener.rb

	cd ${APOLLO_HOME}/examples/stomp/ruby   # 启动一个发送者
	ruby publisher.rb



[1]: http://activemq.apache.org/apollo/download.html