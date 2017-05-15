# gradle 配置 android 项目

## gradle 基本知识 [from][1]
build.gradle 文件分为两种

* Top-Level Build File
* Module-Level Build File

Android Studio 是有控制台可以直接用的.

### 添加依赖的几种方法
1. 直接扔到项目的 `libs/directory` 目录
2. 手工编辑 `build.gradle` 文件
如下:

```
		dependencies {
       compile fileTree(dir: 'libs', include: ['*.jar'])
       compile 'com.google.android.gms:play-services:6.5.+'
    }
```
3. 用 Android Studio 的界面添加 (右键-> Open Module Settings -> Dependencies)


# 其它 gradle 文件

## gradle wrapper [from][2]
gradle-wrapper.properties 会指导 gradle 下载需要用到的 gradle 版本， 一般 android studio 生成维护， 不需要手动改。
`*nix` 系统下, 各种下载的版本会放在 ~/.gradle/wrapper.

## settings.gradle
这个文件包含组成工程的所有模块， 如果只有一个模块， 那文件内容就很简单， 只有一行：

    include ':app'

## gradle.properties
包含应用于整个工程的配置信息，默认是空的。 可以添加很多配置。

## local.properties
这个文件告诉 Android gradle plugin 到哪里找 Android SDK , 例如：

    sdk.dir=/Users/jessica/Library/Android/sdk
这个文件是指每个人本地的安装信息， 所以这个文件不应该放到代码版本管理下。

## 设置 gradle wrapper
在配置文件中添加任务

	task wrapper(type: Wrapper) {
	    gradleVersion = '2.2.1'
	}
执行 `gradle wrapper`

refs:  
[The Ins and Outs of Gradle][1]  



[1]: http://code.tutsplus.com/tutorials/the-ins-and-outs-of-gradle--cms-22978
[2]: https://guides.codepath.com/android/Getting-Started-with-Gradle#intro-to-gradle
