# maven 多模块
*eclipse的maven插件可以方便的创建子模块, 父模块等*

## 父模块
1. 父模块的packaging类型必须是pom, 在modules元素中申明子模块
2. 父模块在dependencyManagement元素中可以统一地管理版本信息, 子模块不管版本
3. pluginManagement,  在父类中定义 plugin 配置, 在子类中引用. [元素介绍][3]  
4. 需要直接子模块继承的plugin不放在pluginManagement中, 直接放在plugins元素中



示例文件:

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
		<modelVersion>4.0.0</modelVersion>
		<groupId>com.zhch</groupId>
		<artifactId>zhch-templet</artifactId>
		<version>0.0.1-SNAPSHOT</version>
		<packaging>pom</packaging>
		<modules>
			<module>zhch-templet-user-dubbo</module>
		</modules>
		<dependencyManagement>
			<dependencies>
				<dependency>
					<groupId>org.springframework</groupId>
					<artifactId>spring-context</artifactId>
					<version>3.1.4.RELEASE</version>
				</dependency>
			</dependencies>
		</dependencyManagement>
		
		<build>
			<!-- 子模块直接继承的 -->
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-deploy-plugin</artifactId>
					<configuration>
						<skip>true</skip>
					</configuration>
				</plugin>
			</plugins>
			<!-- 子模块需要引用才使用的 -->
			<pluginManagement>
				<plugins>
					<plugin>
						<groupId>org.apache.maven.plugins</groupId>
						<artifactId>maven-compiler-plugin</artifactId>
						<version>2.3.2</version>
						<configuration>
							<source>1.6</source>
							<target>1.6</target>
						</configuration>
					</plugin>

				</plugins>
			</pluginManagement>
		</build>
	</project>
## 子模块
1. 子模块在parent元素中申明父模块的标识, 子模块覆盖父模块的packaging属性(jar, war, 也可以是pom)



示例文件:

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
		<modelVersion>4.0.0</modelVersion>
		<parent>
			<groupId>com.zhch</groupId>
			<artifactId>zhch-templet</artifactId>
			<version>0.0.1-SNAPSHOT</version>
		</parent>
		<packaging>war</packaging>
		<artifactId>zhch-templet-user-dubbo</artifactId>
	</project>

## 版本定义的继承

refs:
[Guide to Working with Multiple Modules][1]  
[ Multi-module Project][2]  
[关于pluginManagement][3]  




[1]: http://maven.apache.org/guides/mini/guide-multiple-modules.html
[2]: http://books.sonatype.com/mvnex-book/reference/multimodule.html
[3]: http://maven.apache.org/pom.html#Plugin%5FManagement
