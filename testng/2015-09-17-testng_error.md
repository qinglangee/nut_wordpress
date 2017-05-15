# testng 的一些错误信息

## java.lang.ClassFormatError: Absent Code attribute in method that is not native or abstract in class file。。。。

java.lang.ClassFormatError: Absent Code attribute in method that is not native or abstract in class file  javax/mail/MessagingException
基本上就是 javaee api 中的接口没有实现类， test的时候就找不到类， 把pom.xml的的 javaeeapi 引用的换成一个具体server并把javaee api引用去掉就可以了， 比如用 jetty.

		<dependency>
			<!-- fot test of javaee-api, 代替 javaee-api, 运行测试会用到 -->
			<groupId>org.eclipse.jetty</groupId>
			<artifactId>jetty-server</artifactId>
			<version>9.3.0.M2</version>
		</dependency>

		
answer from [csdn][1]

This problem is likely the result of having the javax:javeee-api(or javax:javaee-web-api) library on your test classpath. If you have a Mavenproject, you likely have the following dependency in your POM file:
 
	<dependency>   <groupId>javax</groupId>   <artifactId>javaee-api</artifactId>   <version>6.0</version></dependency>
This dependency provides you with the Java EE APIs, not theimplementations. While this dependency works for compiling, it cannot be usedfor executing code (that includes tests).

answer from [oracle][2]


[1]: http://blog.csdn.net/beyond667/article/details/8366010
[2]: http://www.oracle.com/technetwork/articles/java/unittesting-455385.html
