# activemq 看过的文档 

[ Features > Persistence > AMQ Message Store][1]
AcitveMQ 5默认用 Kaha做持久化存储. 它是先写到日志里, 再写到数据库里.  
配置文件: 

	<broker brokerName="broker" persistent="true" useShutdownHook="false">
	   <persistenceAdapter>
	     <amqPersistenceAdapter directory="${activemq.base}/activemq-data" maxFileLength="32mb"/>
	   </persistenceAdapter>
	   <transportConnectors>
	     <transportConnector uri="tcp://localhost:61616"/>
	   </transportConnectors>
	 </broker>


[1]: http://activemq.apache.org/amq-message-store.html
