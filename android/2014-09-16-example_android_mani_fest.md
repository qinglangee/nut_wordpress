# AndroidManiFest示例文件

	<?xml version="1.0" encoding="utf-8"?>
	<manifest xmlns:android="http://schemas.android.com/apk/res/android"
	    package="com.l99.bed"
	    android:installLocation="auto"
	    android:versionCode="25"
	    android:versionName="3.0.1">

	    <uses-sdk android:minSdkVersion="8" />

	    <!-- Required  一些系统要求的权限，如访问网络等 -->
	    <uses-permission android:name="com.l99.bed.permission.JPUSH_MESSAGE" />
	    <uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
	    <uses-permission android:name="android.permission.WAKE_LOCK" />
	    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
	    <!-- Optional for location -->
	    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />

	    <!-- Push service 运行需要的权限 -->
	    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
	    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
	    <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
	    <!-- Push service 运行需要的权限end -->

	    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
	    <uses-permission android:name="android.permission.KILL_BACKGROUND_PROCESSES" />
	    <uses-permission android:name="android.permission.READ_CONTACTS" /> 
	    <uses-permission android:name="android.permission.RESTART_PACKAGES" />
	    <uses-permission android:name="android.permission.VIBRATE" />
	    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	    <uses-permission android:name="android.permission.READ_LOGS" />
	    <uses-permission android:name="android.permission.INTERNET" />
	    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
	    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
	    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	    <uses-permission android:name="android.permission.BROADCAST_STICKY" />
	    <uses-permission android:name="android.permission.RECORD_AUDIO" />
	    <uses-permission android:name="android.permission.CAMERA" />
	    <uses-permission android:name="android.permission.GET_TASKS" />
	    <!-- 百度定位SDK增加的权限 -->
	    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
	    <!-- 高德定位api需要的权限 -->
	    <uses-permission android:name="android.permission.CHANGE_CONFIGURATION" />
	    <uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS" />
	    <uses-permission android:name="android.permission.ACCESS_MOCK_LOCATION" />
	    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
	    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
	    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />

	    <!-- 【可选】 信鸽SDK所需权限 -->
	    <uses-permission android:name="android.permission.BLUETOOTH" />
	    <uses-permission android:name="android.permission.BATTERY_STATS" />

	    <compatible-screens>
	        <screen
	            android:screenDensity="mdpi"
	            android:screenSize="normal" />
	        <screen
	            android:screenDensity="hdpi"
	            android:screenSize="normal" />
	        <screen
	            android:screenDensity="xhdpi"
	            android:screenSize="normal" />
	        <screen
	            android:screenDensity="mdpi"
	            android:screenSize="large" />
	        <screen
	            android:screenDensity="hdpi"
	            android:screenSize="large" />
	        <screen
	            android:screenDensity="xhdpi"
	            android:screenSize="large" />
	        <screen
	            android:screenDensity="mdpi"
	            android:screenSize="xlarge" />
	        <screen
	            android:screenDensity="hdpi"
	            android:screenSize="xlarge" />
	        <screen
	            android:screenDensity="xhdpi"
	            android:screenSize="xlarge" />
	    </compatible-screens>

	    <application
	        android:hardwareAccelerated="true"
	        android:name="com.l99.DoveboxApp"
	        android:allowBackup="true"
	        android:icon="@drawable/ic_launcher"
	        android:label="@string/app_name"
	        android:largeHeap="true" >
	        <uses-library
	            android:name="com.google.android.maps"
	            android:required="false" />

	        <meta-data
	            android:name="com.amap.api.v2.apikey"
	            android:value="@string/abc_map_api_key" />

	        <service android:name="com.l99.ui.musicplayer.service.MusicPlayService" />

	        <activity
	            android:name="com.l99.MainActivity"
	            android:screenOrientation="portrait"
	            android:launchMode="singleTop"
	            android:exported="true">
	        </activity>

			<!-- 入口Activity -->
	        <activity
	            android:name="com.l99.WelcomActivity"
	            android:allowTaskReparenting="true"
	            android:launchMode="singleTop"
	            android:screenOrientation="portrait"
	            android:theme="@android:style/Theme.Translucent.NoTitleBar" >
	            <intent-filter>
	                <action android:name="android.intent.action.MAIN" />

	                <category android:name="android.intent.category.LAUNCHER" />
	            </intent-filter>
	        </activity>
	        <activity
	            android:name="com.l99.ui.chat.activity.ChatRoomActivity"
	            android:launchMode="singleTask"
	            android:screenOrientation="portrait"
	            android:theme="@android:style/Theme.Translucent.NoTitleBar"
	            android:windowSoftInputMode="adjustResize" />
	        <activity
	            android:name="com.l99.ui.dashboard.activity.DashboardContent"
	            android:allowTaskReparenting="true"
	            android:hardwareAccelerated="true"
	            android:launchMode="singleTop"
	            android:exported="true"
	            android:screenOrientation="portrait"
	            android:theme="@android:style/Theme.Translucent.NoTitleBar" />

	        <service android:name="com.l99.ui.chat.utils.AudioPlayService" />
	        <service
	            android:name="com.l99.dovebox.common.httpclient.uploader.Uploader"
	            android:enabled="true"
	            android:exported="false" />

	        <meta-data
	            android:name="UMS_APPKEY"
	            android:value="e5a5544063cd1da3b2b8721eb03434ac" />
	        
	        <activity
	            android:name="com.l99.ui.wx.WXFriendsActivity"
	            android:allowTaskReparenting="true"
	            android:launchMode="singleTask"
	            android:screenOrientation="portrait"
	            android:theme="@android:style/Theme.Translucent" >
	            <intent-filter>
	                <data
	                    android:host="activities"
	                    android:scheme="dovebox" />

	                <category android:name="android.intent.category.BROWSABLE" />
	                <category android:name="android.intent.category.DEFAULT" />

	                <action android:name="android.intent.action.VIEW" />
	            </intent-filter>
	        </activity>

	        <receiver
	            android:name="com.l99.utils.NetWorkChangedReceiver"
	            android:permission="android.permission.ACCESS_NETWORK_STATE" >
	            <intent-filter>
	                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
	            </intent-filter>
	        </receiver>
	        <receiver
	            android:name="com.l99.utils.AppInstallReceiver"
	            android:label="@string/app_name" >
	            <intent-filter>
	                <action android:name="android.intent.action.PACKAGE_ADDED" />
	                <action android:name="android.intent.action.PACKAGE_REPLACED" />
	                <action android:name="android.intent.action.PACKAGE_REMOVED" />

	                <data android:scheme="package" />
	            </intent-filter>
	        </receiver>

	        <!-- jpush -->


	        <!-- 信鸽 -->
	        <!-- handle message -->
	        <receiver android:name="com.l99.utils.MessageReceiver" >
	            <intent-filter>
	                <action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
	                <action android:name="com.tencent.android.tpush.action.FEEDBACK" />
	            </intent-filter>
	        </receiver>
	        
	        <!-- push broadcast -->
	                <receiver
	            android:name="com.tencent.android.tpush.XGPushReceiver"
	            android:process=":xg_service_v2" >
	            <intent-filter android:priority="0x7fffffff" >
	                <!-- 【必须】 信鸽SDK的内部广播 -->
	                <action android:name="com.tencent.android.tpush.action.SDK" />
	                <action android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
	                <!-- 【必须】 系统广播：开屏和网络切换 -->
	                <action android:name="android.intent.action.USER_PRESENT" />
	                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

	                <!-- 【可选】 一些常用的系统广播，增强信鸽service的复活机会，请根据需要选择。当然，你也可以添加APP自定义的一些广播让启动service -->
	                <action android:name="android.intent.action.BOOT_COMPLETED" />
	                <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
	                <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
	                <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
	            </intent-filter>
	            <!-- 【可选】 usb相关的系统广播，增强信鸽service的复活机会，请根据需要添加 -->
	            <intent-filter android:priority="0x7fffffff" >
	                <action android:name="android.intent.action.MEDIA_UNMOUNTED" />
	                <action android:name="android.intent.action.MEDIA_REMOVED" />
	                <action android:name="android.intent.action.MEDIA_CHECKING" />
	                <action android:name="android.intent.action.MEDIA_EJECT" />

	                <data android:scheme="file" />
	            </intent-filter>
	        </receiver>
	        
	        <!-- 【必须】 (2.30及以上版新增)展示通知的activity -->
	    <!-- 【注意】 如果被打开的activity是启动模式为SingleTop，SingleTask或SingleInstance，请根据通知的异常自查列表第8点处理-->
	     <activity
	         android:name="com.tencent.android.tpush.XGPushActivity"
	         android:exported="false" >
	         <intent-filter>
	            <!-- 若使用AndroidStudio，请设置android:name="android.intent.action"-->
	             <action android:name="" />
	         </intent-filter>
	    </activity>
	        
	        <!-- push service -->
	        <service
	            android:name="com.tencent.android.tpush.service.XGPushService"
	            android:exported="true"
	            android:process=":xg_service_v2" />

	        <!-- 【建议】 信鸽service守护进程，可以增加复活机会，提升消息抵达率 -->
	        <service
	            android:name="com.tencent.android.tpush.service.XGDaemonService"
	            android:process=":qq_push_daemon" />
	        
	        
	        <!-- xinge accessid accesskey -->
	        <meta-data    
	            android:name="XG_V2_ACCESS_ID"
	            android:value="2100046275" />
	        <!-- xinge渠道 -->
	        <meta-data
	            android:name="XG_V2_ACCESS_KEY"
	            android:value="ACK3R83J3E7S" />
	    </application>

	</manifest>
