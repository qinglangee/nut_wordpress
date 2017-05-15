# gradle 错误 

## 导入eclipse 时报错
> SDK locateon not found.

设置 ANDROID_HOME 环境变量 , 或在 local.properties中设置 sdk.dir, 重启Eclipse
以上都设置了还是报这个错时, 有可能是各个项目依赖的问题, 把项目单独放到一个目录导入.

开始报另一个错了
> eclipse  plugin with id "com.android.library" not found