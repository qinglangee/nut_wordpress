# gradle 设置使用maven仓库

在用户目录下创建~/.gradle/init.gradle，内容如下:

	allprojects {
	    repositories {
	        mavenLocal()
	        maven {
	          name 'oschina'
	          url "http://maven.oschina.net/content/groups/public/"
	        }
	        maven {
	          url "http://localhost:8081/nexus/content/groups/public/"
	        }
	    }
	}

把想要先访问的库放在前面。


refs:  
[Gradle设置全局仓库 ](http://my.oschina.net/ekuma/blog/298009)