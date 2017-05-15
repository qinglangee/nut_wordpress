# Missing artifact com.sun:tools:jar:1.5.0:system 解决方法

## 解决方案一：
原来，是${java.home}在作怪，eclipse 没有使用 JAVA_HOME
默认，eclipse 使用 C:"windows"system32"javaw.exe 作为 JVM，当然找不到tools.jar

解决方法如下：
修改 eclipse.exe 目录下的 eclipse.ini 指定vm，，注意 -vm后面不能有空格。

-vmD:\Program Files\Java\jdk1.6.0_23\bin\javaw.exe
-vmargs
-Dosgi.requiredJavaVersion=1.5
-Xms40m
-Xmx512m
-XX:PermSize=64M
-XX:MaxPermSize=512M

## 解决方案二：

配置pom.xml文件

 

    <properties>
	    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	    <spring.version>3.0.5.RELEASE</spring.version>
	    <java.home>jdk路径</java.home>
    </properties>
    <profiles>
	    <profile>
		    <id>default-tools.jar</id>
		    <activation>
			    <property>
				    <name>java.vendor</name>
				    <value>Sun Microsystems Inc.</value>
			    </property>
		    </activation>
		    <dependencies>
			    <dependency>
				    <groupId>com.sun</groupId>
				    <artifactId>tools</artifactId>
				    <version>1.5.0</version>
				    <scope>system</scope>
				    <systemPath>${java.home}/lib/tools.jar</systemPath>
			    </dependency>
		    </dependencies>
	    </profile>
    </profiles>

在pom.xml文件中将这段配置写上，试一下。注意几个位置的内容编写。 