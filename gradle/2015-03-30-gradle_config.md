# gradle 配置

## 加速　gradle 编译
In Android Studio, open the gradle.properties file in the project and add:

		#开启后台进程
		org.gradle.daemon=true
		# 调整堆栈大小适合你的项目编译
		org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
		# 把你的项目模块化，开启并行构建
		org.gradle.parallel=true

		# Enable configure on demand.
		org.gradle.configureondemand=true
[Getting Started with Gradle][1]，　原文中还有一些其它的方法，　可以去看看链接　

## 实现 maven copy-dependencies

	apply plugin: 'java'

	repositories {
	   mavenCentral()
	}

	dependencies {
	   compile 'com.google.inject:guice:4.0-beta5'
	}

	task copyDependencies(type: Copy) {
	   from configurations.compile
	   into 'dependencies'
	}



refs:  
[Getting Started with Gradle][1]
[1]: https://guides.codepath.com/android/Getting-Started-with-Gradle#intro-to-gradle
