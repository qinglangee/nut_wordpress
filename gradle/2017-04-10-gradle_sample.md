# gradle 配置文件示例
// Top-level build file where you can add configuration options common to all sub-projects/modules.
顶级构建文件 Top Level build file:

    buildscript {
        repositories {
            jcenter()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:2.2.+'
            // NOTE: Do not place your application dependencies here; they belong
            // in the individual module build.gradle files
        }
    }
     
    allprojects {
        repositories {
            // 配置优先使用本地 maven 仓库
            mavenLocal()
            jcenter()
            maven {
                // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
                url "$rootDir/../node_modules/react-native/android"
            }
        }
    }

模块级别的构建文件 Module-Level Gradle Build Files：

    apply plugin: 'com.android.application'
          
    // 因为是 android 应用必须用 android 插件
    android {
     
        compileSdkVersion 21          //The API your project is targeting.// 
     
        buildToolsVersion "21.1.1"    ////The version of the build tools you want to use.//
     
        defaultConfig {
            /Defines your application’s ID. Note, earlier versions of the Android plugin used ‘packageName’ instead of ‘applicationID.’//
            applicationId "com.example.jessica.myapplication"
     
            minSdkVersion 16           //The minimum API required by your project.//
     
            targetSdkVersion 21        //The version of Android you’re developing your application for.//
             
            versionCode 1
     
            versionName "1.0"
        }
        
        //‘BuildTypes’ 控制你的APP 怎样构建和打包. If you want to create your own build variants, you’ll need to add them to this section.//
        buildTypes {
            release {
     
                minifyEnabled true         //Gradle runs ProGuard during the build process.//
                
                //Applies the default ProGuard settings from the Android SDK.// 
                proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
     
            }
        }
    }
     
    dependencies {
        //你可以单独地添加jar文件，比较麻烦嘛。 这个示例添加 app/libs 目录下所有 jar 文件
        compile fileTree(dir: 'libs', include: ['*.jar'])
     
        //To create more dependencies, add them to the depencies closure.//
        compile 'com.android.support:appcompat-v7:21.0.3'
     
    }