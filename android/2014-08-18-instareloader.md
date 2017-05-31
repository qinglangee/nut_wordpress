# 动态加载android

## 部署步骤
Let’s start from the clean project in the Eclipse:


1. 创建 ${USER_HOME}/InstaReloader/instareloader.props , 定义 Android SDK 和项目路径.
2. 为你的项目创建一个Android测试项目.
3. 修改测试项目的 AndroidManifex.xml(在配置页面下载模板), 把InstaReloader-client.jar 放到libs目录.

*IMPORTANT: 你的工程和测试工程必须有相同的 android:sharedUserId*

4. 启动 InstaReloader server .

5. 用InstaReloader启动你的工程: 在菜单中选择 “run as Android app” 

6. app成功启动后会有弹出消息. 

device-2013-12-23-223515

服务端会显示有app连接. 


7. Enjoy code hot swapping on the Android.

Check the [Help][2] page if you have any troubles


refs:  
[Enabling InstaReloader in Eclipse IDE][1]

[1]: http://www.instareloader.com/enabling-instareloader-in-the-eclipse-ide/
[2]: http://www.instareloader.com/help/