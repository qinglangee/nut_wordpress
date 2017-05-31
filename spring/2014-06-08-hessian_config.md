# spring 中配置 hessian

## 配置web.xml，利用dispatchServlet处理请求
web.xml, 配置servlet 路径, 以spring DispatcherServlet 处理.

	<servlet>
		<servlet-name>spring</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:spring-servlet.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>spring</servlet-name>
		<url-pattern>/hessian/*</url-pattern>
	</servlet-mapping>

参数 contextConfigLocation 的默认值是 WEB-INF 目录下的 spring-servlet.xml (`<servlet-name>`再加 "-servlet.xml" 后缀), 如果位置或文件名不是默认值就需要明确指定.
# 普通 hessian 配置

## pom.xml hessian

	<dependency>
		<groupId>com.caucho</groupId>
		<artifactId>hessian</artifactId>
		<version>4.0.7</version>
	</dependency>
## web.xml

	<servlet>
		<servlet-name>myservice</servlet-name>
		<servlet-class>com.caucho.hessian.server.HessianServlet</servlet-class>
		<init-param>
			<param-name>service-class</param-name>
			<param-value>com.abcd.web.myservice.MyServiceAction</param-value>
		</init-param>
	</servlet>
	<servlet-mapping>
		<servlet-name>myservice</servlet-name>
		<url-pattern>/myservice</url-pattern>
	</servlet-mapping>
## 实现类 MyServiceAction

	package com.abcd.web.myservice;

	public class MyServiceAction implements MyServiceActionIF{

		public long delete(int id) {
			return 1234L;
		}

	}
MyServiceActionIF 接口中定义了hessian对外提供的方法

	package com.abcd.web.myservice;

	public interface MyServiceActionIF {
		public long delete(int id);
	}

## 客户端
客户端利用 DashboardActionIF 接口, 从url指定的服务处调用.

	package com.abcd.web.myservice;

	import java.net.MalformedURLException;

	import com.caucho.hessian.client.HessianProxyFactory;

	public class MyServiceClient {

		private static HessianProxyFactory factory = null;
		private static MyServiceActionIF service;
		
		public static void init(String url){
			String urlPath = url;
			factory = new HessianProxyFactory();
			factory.setOverloadEnabled(true);
			factory.setConnectTimeout(3000);
			try {
				service = (MyServiceActionIF) factory.create(MyServiceActionIF.class, urlPath);
			} catch (MalformedURLException e) {
				e.printStackTrace();
			}
		}

		
		public static long delete(int id) {
			return service.delete(id);
		}
		
		public static void main(String[] args) {
			MyServiceClient.init("http://192.168.50.124:8680/testweb/myservice");
			long aa = MyServiceClient.delete(90);
			System.out.println("aa: " + aa);
		}
	}
