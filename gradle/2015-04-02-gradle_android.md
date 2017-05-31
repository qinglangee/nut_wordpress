# gradle 运行 android


## 依赖本地文件

	dependencies {
		compile fileTree(dir: 'libs', include: '*.jar')
	}
## 下载android support

	compile 'com.android.support:appcompat-v7:19.+'
## 修改默认目录 [gradle目录结构][1]

	sourceSets {
	    main {
	        java {
	            srcDir 'src/java'
	        }
	        resources {
	            srcDir 'src/resources'
	        }
	    }
	}

## 依赖其它项目, [as dependency][2]  

1. 如果是依赖子项目, 在`Project/settings.gradle` 中

添加

	include ':Dependency'
在`Project/build.gradle` 依赖部分添加

	dependencies {
	   compile project(':Dependency')
	}
2. 不是子项目

Project/settings.gradle

	include ':Dependency'
	project(':Dependency').projectDir = new File(settingsDir, '../Dependency')

Project/build.gradle

	dependencies {
	   compile project(':Dependency')
	}

## 打包 library








refs:  
[Gradle Plugin User Guide](http://tools.android.com/tech-docs/new-build-system/user-guide)   
[gradle Eclipse 插件文档](https://github.com/spring-projects/eclipse-integration-gradle/wiki)  
[Compile gradle project with another project as a dependency][2]  
[gradle build 官方文档][3]  
[一个eclipse插件带的旧的模板文件][12]  
[旧版到新版的迁移][13]  




[1]: http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Project-Structure
[2]: http://www.tuicool.com/articles/RZRBvej
[3]: http://tools.android.com/tech-docs/new-build-system/user-guide


[12]: https://github.com/Nodeclipse/nodeclipse-1/blob/master/org.nodeclipse.enide.editors.gradle/docs/android/build.gradle
[13]: http://tools.android.com/tech-docs/new-build-system/migrating-to-1-0-0