# Android 处理运行时状态改变
android 的一些设置配置会在运行时改变(如横竖方向, 键盘, 语言).
当遇到这些改变时, Android系统会重启 Activity (onDestroy -> onCreate).
重启是为了帮助应用适应新的配置(如重新设置 alternative resources).
如果你的应用重启消耗很多资源的话, 可以用下面两种方式来处理
## 用Fragment保存状态

1. 继承 Fragment 类, 声明要保留状态的对象. 
2. 在Fragment create的时候调用 setRetainInstance(boolean).
3. 把 fragment 添加到 activity.
4. activity 重新启动时用 FragmentManager 来重新取到 fragment. 

*Caution:* 不能保存任何与 context 相关的对象, 会导致内存泄露. 
示例, android_demo -> StateFrag
## 拦截状态改变事件, 自己处理

用了这个后系统不会自动处理activity, 也不自动应用 alternative resources. 
所以能不用尽量不用. 以下这两个是比较常用的选项:

	<activity android:name=".MyActivity"
	          android:configChanges="orientation|keyboardHidden|screenSize"
	          android:label="@string/app_name">
配置之后状态改变时, 系统会调用 activity 的 ` onConfigurationChanged()` 方法. 在这个方法中自己处理状态改变.
*Caution:* 版本13开始 screenSize 在orientation改变时也会改变.

	@Override
	public void onConfigurationChanged(Configuration newConfig) {
	    super.onConfigurationChanged(newConfig);

	    // Checks the orientation of the screen
	    if (newConfig.orientation == Configuration.ORIENTATION_LANDSCAPE) {
	        Toast.makeText(this, "landscape", Toast.LENGTH_SHORT).show();
	    } else if (newConfig.orientation == Configuration.ORIENTATION_PORTRAIT){
	        Toast.makeText(this, "portrait", Toast.LENGTH_SHORT).show();
	    }
	}
具体 Configuration 的各个值可以查看 JAVA DOC [Configuration][1].  


refs:  
[Handling Runtime Changes](http://developer.android.com/guide/topics/resources/runtime-changes.html)  




[1]: http://developer.android.com/reference/android/content/res/Configuration.html