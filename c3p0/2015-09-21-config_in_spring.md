# c3p0 在 spring 中的配置

spring-hibernate.xml

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:tx="http://www.springframework.org/schema/tx"
		xmlns:aop="http://www.springframework.org/schema/aop" xmlns:context="http://www.springframework.org/schema/context"
		xsi:schemaLocation="
	http://www.springframework.org/schema/beans 
	http://www.springframework.org/schema/beans/spring-beans.xsd 
	http://www.springframework.org/schema/tx 
	http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
	http://www.springframework.org/schema/aop 
	http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context-3.0.xsd
	">


		<!-- spring使用注解创建实例 -->
		<context:component-scan base-package="com.ison.*"></context:component-scan>

		<!-- 配置数据源 -->
		<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"

			destroy-method="close">

			<property name="driverClass" value="com.mysql.jdbc.Driver" />
			<property name="jdbcUrl"
				value="jdbc:mysql://localhost:3306/resume_import_sys?useUnicode=true&amp;characterEncoding=utf-8" />

			<property name="user" value="root"/>
			<property name="password" value="zhch"/>

			<!--连接池中保留的最小连接数。 -->
			<property name="minPoolSize" value="5"/>

			<!--连接池中保留的最大连接数。Default: 15 -->
			<property name="maxPoolSize" value="40"/>

			<!--初始化时获取的连接数，取值应在minPoolSize与maxPoolSize之间。Default: 3 -->
			<property name="initialPoolSize" value="10"/>

			<!--最大空闲时间,60秒内未使用则连接被丢弃。若为0则永不丢弃。Default: 0 -->
			<property name="maxIdleTime" value="60"/>

			<!--当连接池中的连接耗尽的时候c3p0一次同时获取的连接数。Default: 3 -->
			<property name="acquireIncrement" value="5"/>

			<!--JDBC的标准参数，用以控制数据源内加载的PreparedStatements数量。但由于预缓存的statements 属于单个connection而不是整个连接池。所以设置这个参数需要考虑到多方面的因素。 
				如果maxStatements与maxStatementsPerConnection均为0，则缓存被关闭。Default: 0 -->
			<property name="maxStatements" value="0"/>

			<!--每60秒检查所有连接池中的空闲连接。Default: 0 -->
			<property name="idleConnectionTestPeriod" value="180"/>

			<!--定义在从数据库获取新连接失败后重复尝试的次数。Default: 30 -->
			<property name="acquireRetryAttempts" value="30"/>

			<!--获取连接失败将会引起所有等待连接池来获取连接的线程抛出异常。但是数据源仍有效 保留，并在下次调用getConnection()的时候继续尝试获取连接。如果设为true，那么在尝试 
				获取连接失败后该数据源将申明已断开并永久关闭。Default: false -->
			<property name="breakAfterAcquireFailure" value="true"/>

			<!--因性能消耗大请只在需要的时候使用它。如果设为true那么在每个connection提交的 时候都将校验其有效性。建议使用idleConnectionTestPeriod或automaticTestTable 
				等方法来提升连接测试的性能。Default: false -->
			<property name="testConnectionOnCheckout" value="false"/>

		</bean>



		<!-- 配置hibernate session工厂 -->
		<bean id="sessionFactory"
			class="org.springframework.orm.hibernate4.LocalSessionFactoryBean">
			<property name="dataSource" ref="dataSource" />
			<property name="hibernateProperties">
				<props>
					<prop key="hibernate.hbm2ddl.auto">update</prop>
					<prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
					<prop key="hibernate.current_session_context_class">org.springframework.orm.hibernate4.SpringSessionContext
					</prop>
					<prop key="hibernate.show_sql">false</prop>
					<prop key="hibernate.format_sql">false</prop>
				</props>
			</property>

			<!-- 自动扫描注解方式配置的hibernate类文件 -->
			<property name="packagesToScan">
				<list>
					<value>com.ison.bean..</value>
				</list>
			</property>
		</bean>

		<bean id="hibernateTemplate" class="org.springframework.orm.hibernate4.HibernateTemplate">
			<property name="sessionFactory" ref="sessionFactory" />
		</bean>

		<!-- 配置事务管理器 -->
		<bean name="transactionManager"
			class="org.springframework.orm.hibernate4.HibernateTransactionManager">
			<property name="sessionFactory" ref="sessionFactory"></property>
		</bean>

		<!-- 注解方式配置事物 -->
		<!-- <tx:annotation-driven transaction-manager="transactionManager" /> -->

		<!-- 拦截器方式配置事物 -->
		<tx:advice id="transactionAdvice" transaction-manager="transactionManager">
			<tx:attributes>
				<tx:method name="save*" propagation="REQUIRED" />
				<tx:method name="add*" propagation="REQUIRED" />
				<tx:method name="update*" propagation="REQUIRED" />
				<tx:method name="delete*" propagation="REQUIRED" />
				<tx:method name="find*" read-only="true" />
				<tx:method name="*" read-only="true" />
			</tx:attributes>
		</tx:advice>
		<aop:config>
			<aop:pointcut id="transactionPointcut" expression="execution(* com.ison.service..*.*(..))" />
			<aop:advisor pointcut-ref="transactionPointcut"
				advice-ref="transactionAdvice" />
		</aop:config>


	</beans>


refs:  
[c3p0 官方文档][1]  
[c3p0详细配置](http://www.blogjava.net/ashutc/archive/2015/03/12/346365.html#423415)  

[1]: http://www.mchange.com/projects/c3p0/index.html