# pom 示例文件

打包的名字， profile 之类

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
		<modelVersion>4.0.0</modelVersion>
		<parent>
			<groupId>com.zc</groupId>
			<artifactId>exp</artifactId>
			<version>0.0.1-SNAPSHOT</version>
		</parent>
		<artifactId>exp-user-war</artifactId>
		<packaging>war</packaging>


		<properties>
			<!-- 设置编码 -->
			<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
			<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
			<java.version>1.7</java.version>
			<docker.image.prefix>registry-internal.cn-beijing.aliyuncs.com/designer</docker.image.prefix>
		</properties>

		<profiles>
			<profile>
				<id>development</id>
				<activation>
					<activeByDefault>true</activeByDefault>
				</activation>
				<properties>
					<deployer.enviroment>development</deployer.enviroment>
				</properties>
				<build>
					<!-- 定义最终打包产生的名字 -->
					<finalName>${project.artifactId}</finalName>
					<resources>
						<resource><!-- 资源文件目录, 可以指定多个, 默认是  src/main/resources -->
							<directory>src/main/resources</directory>
							<includes>
								<include>*</include>
							</includes>
							<filtering>true</filtering>
						</resource>
						<resource>
							<directory>src/main/java</directory>
							<excludes>
								<exclude>**/*.java</exclude>
							</excludes>
							<filtering>true</filtering>
						</resource>
					</resources>
				</build>
			</profile>
			<!-- 不同的配置文件 profile, 在 maven 编译时 用 -P production 指定使用哪个配置 -->
			<profile>
				<id>production</id>
				<properties>
					<deployer.enviroment>production</deployer.enviroment>
				</properties>
			</profile>
		</profiles>
		<dependencies>
			<!-- 指定一个由容器提供的包, 在打包时不打包到结果中 -->
			<dependency>
				<groupId>javaee</groupId>
				<artifactId>javaee-api</artifactId>
				<version>5</version>
				<scope>provided</scope>
			</dependency>

			<!-- fot test of javaee-api, 可以用来代替 javaee-api, 运行测试会用到 -->
			<dependency>
				<groupId>org.eclipse.jetty</groupId>
				<artifactId>jetty-server</artifactId>
				<version>9.3.0.M2</version>
				<scope>provided</scope>
			</dependency>
		</dependencies>
	</project>


在使用maven构建项目的时候，maven使用了它自己的结构：
src
  |-main
  |  |- java
  |  |- resource
     |- webapp
           |- WEB-INF

但如果使用wtp dyna web project的时候，生成的目录结构则与此不同，在使用一些maven插件，如mvn war:inplace的时候，maven代仍为按照自身默认的结构来拷贝相应的jar包到lib目录下。为了使maven能够符合自己定义的目录结构，则需要使用一些插件来定制,下面给出一个符合WTP目录结构的pom.xml配置文件：


	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	    <modelVersion>4.0.0</modelVersion>
	    <groupId>cust_project</groupId>
	    <artifactId>cust_project</artifactId>
	    <packaging>war</packaging>
	    <version>0.0.1-SNAPSHOT</version>
	    <build>
	        <plugins>
	            <plugin>
	                <groupId>org.apache.maven.plugins</groupId>
	                <artifactId>maven-compiler-plugin</artifactId>
	                <configuration>
	                    <source>1.5</source>
	                    <target>1.5</target>
	                    <encoding>UTF-8</encoding>
	                </configuration>
	            </plugin>
	            <plugin>
	                <groupId>org.codehaus.mojo</groupId>
	                <artifactId>build-helper-maven-plugin</artifactId>
	                <version>1.1</version>
	                <executions>
	                    <execution>
	                        <id>add-source</id>
	                        <phase>generate-sources</phase>
	                        <goals>
	                            <goal>add-source</goal>
	                        </goals>
	                        <configuration>
	                            <sources>
	                                <source>src/java</source>
	                                <source>src/resources</source>
	                            </sources>
	                        </configuration>
	                    </execution>
	                </executions>
	            </plugin>
	            <plugin>
	                <groupId>org.apache.maven.plugins</groupId>
	                <artifactId>maven-war-plugin</artifactId>
	                <configuration>
	                    <!-- 设置WebContent目录为Web目录 -->
	                    <warSourceDirectory>WebContent</warSourceDirectory>
	                </configuration>
	            </plugin>
	        </plugins>
	        <outputDirectory>WebContent/WEB-INF/classes</outputDirectory>
	    </build>
	    <dependencies>
	    	<!-- J2EE 需要的包 -->
	        <dependency>
				<groupId>javaee</groupId>
				<artifactId>javaee-api</artifactId>
				<version>5</version>
				<scope>provided</scope>
			</dependency>
			<dependency>
				<groupId>javax.servlet</groupId>
				<artifactId>jstl</artifactId>
				<version>1.2</version>
				<scope>provided</scope>
			</dependency>

	    </dependencies>
	</project>

发布自己的包， 配置 distributionManagement，直接在根元素 `<project>` 中。  
id 在 settings.xml 中配置


	<distributionManagement>
		<repository>
			<id>localRelease</id>
			<url>http://192.168.0.55:8081/nexus/content/repositories/releases/</url>
		</repository>
		<snapshotRepository>
			<id>localSnapshot</id>
			<url>http://192.168.0.55:8081/nexus/content/repositories/snapshots/</url>
		</snapshotRepository>
	</distributionManagement>
