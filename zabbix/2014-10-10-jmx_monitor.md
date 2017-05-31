# 设置 JMX 监控

zabbix 2.0开始, 监控JMX 可以通过 Zabbix Java gateway, 之前的版本需要 app 里自己加入编码.
## 安装 Java gateway

下载zabbix源码, 带 java参数编译

	$ ./configure --enable-java
	$ make
生成的内容在 src/zabbix_java 目录中, 可以直接在这个目录中使用, 也可以用 `make install` 命令安装  

生成的文件有:

>*运行的jar文件*  
bin/zabbix-java-gateway-$VERSION.jar  
*依赖文件*  (note that up to Zabbix 2.2.5 JSON.org library was used).  
lib/logback-core-0.9.27.jar
lib/logback-classic-0.9.27.jar
lib/slf4j-api-1.6.1.jar
lib/android-json-4.3_r3.1.jar
*logback配置文件*  
lib/logback.xml  
lib/logback-console.xml
*启动/停止 脚本*
shutdown.sh  
startup.sh
*启动/停止 脚本会引用的配置文件*
settings.sh

默认监听端口 10052

	$ ./startup.sh
	$ ./shutdown.sh
## 配置 java gateway

在server配置文件 */etc/zabbix/zabbix_server.conf* 中指定 ip, port, StartJavaPollers

	JavaGateway=192.168.3.14
	JavaGatewayPort=10052
	StartJavaPollers=5


## 启动 应用的 JMX 远程监控功能 
用以下参数启动应用

	java \
	-Dcom.sun.management.jmxremote \
	-Dcom.sun.management.jmxremote.port=12345 \
	-Dcom.sun.management.jmxremote.authenticate=false \
	-Dcom.sun.management.jmxremote.ssl=false \
	-jar /usr/share/doc/openjdk-6-jre-headless/demo/jfc/Notepad/Notepad.jar
下面的配置增加了验证, 并可以在localhost以外监控

	java \
	-Djava.rmi.server.hostname=192.168.3.14 \
	-Dcom.sun.management.jmxremote \
	-Dcom.sun.management.jmxremote.port=12345 \
	-Dcom.sun.management.jmxremote.authenticate=true \
	-Dcom.sun.management.jmxremote.password.file=/etc/java-6-openjdk/management/jmxremote.password \
	-Dcom.sun.management.jmxremote.access.file=/etc/java-6-openjdk/management/jmxremote.access \
	-Dcom.sun.management.jmxremote.ssl=true \
	-Djavax.net.ssl.keyStore=$YOUR_KEY_STORE \
	-Djavax.net.ssl.keyStorePassword=$YOUR_KEY_STORE_PASSWORD \
	-Djavax.net.ssl.trustStore=$YOUR_TRUST_STORE \
	-Djavax.net.ssl.trustStorePassword=$YOUR_TRUST_STORE_PASSWORD \
	-Dcom.sun.management.jmxremote.ssl.need.client.auth=true \
	-jar /usr/share/doc/openjdk-6-jre-headless/demo/jfc/Notepad/Notepad.jar
_Note that if you wish to use SSL, you have to modify startup.sh script by adding -Djavax.net.ssl.* options to Java gateway, so that it knows where to find key and trust stores._

## 添加 JMX agent item

1. 在host 配置页面, 添加一个 JMX interfaces (填写IP, 端口).  
2. 添加item  




refs:  
[14 JMX monitoring][1]  
[5 Java gateway][2]   



[1]: https://www.zabbix.com/documentation/2.2/manual/config/items/itemtypes/jmx_monitoring
[2]: https://www.zabbix.com/documentation/2.2/manual/concepts/java