# dubbo 常用配置


## 配置dubbo从不同的zookeeper 取service
在每个 `<dubbo:protocol>`的配置前设置不同的zookeeper就行了

	<dubbo:monitor protocol="registry" />
	<!-- 默认注册中心 -->
	<dubbo:registry protocol="zookeeper" address="192.168.2.144:2181" client="zkclient" />
	
	<dubbo:protocol name="dubbo" port="20880" />
## 配置dubbo注册到不同的group