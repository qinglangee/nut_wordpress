# tomcat web.xml 配置模板



	<?xml version="1.0" encoding="UTF-8"?>
	<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
		http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
		<display-name></display-name>
		<!-- spring配置文件位置 -->
		<context-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:spring-*.xml</param-value>
		</context-param>

		<!-- sprint mvc servlet -->
		<servlet>
			<servlet-name>spring</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<load-on-startup>1</load-on-startup>
		</servlet>

		<servlet-mapping>
			<servlet-name>spring</servlet-name>
			<url-pattern>/resume/*</url-pattern>
		</servlet-mapping>

		<!-- Struts2配置 -->
		<filter>
			<filter-name>struts2</filter-name>
			<filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
		</filter>
		<filter-mapping>
			<filter-name>struts2</filter-name>
			<url-pattern>/web/*</url-pattern>
		</filter-mapping>

		<!-- 设置编码 -->
		<filter>
			<filter-name>Character Encoding</filter-name>
			<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
			<init-param>
				<param-name>encoding</param-name>
				<param-value>UTF-8</param-value>
			</init-param>
		</filter>
		<filter-mapping>
			<filter-name>Character Encoding</filter-name>
			<url-pattern>/*</url-pattern>
		</filter-mapping>

		<!-- spring监听器 -->
		<listener>
			<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
		</listener>
		<!-- 自定义 listener -->
		<listener>
			<listener-class>com.ison.server.ServerStartupListener</listener-class>
		</listener>


		<welcome-file-list>
			<welcome-file>/index.htm</welcome-file>
			<welcome-file>/index.html</welcome-file>
			<welcome-file>/index.jsp</welcome-file>
		</welcome-file-list>
	</web-app>

实现一个servlet context listener

	public class ServerStartupListener implements ServletContextListener {}