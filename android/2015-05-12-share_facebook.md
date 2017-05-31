# 分享到facebook

主要步骤:

1. 添加Facebook的SDK
2. 注册一个 Facebook App ID, 配置到 AndroidManifest.xml. (一定要 @string/app_id)
3. 生成一个签名 hash, 配置到facebook developer profile
4. 添加 Facebook Activity 到 AndroidManifest.xml
5. You also need to set up a ContentProvider in your AndroidManifest.xml where {APP_ID} is your app ID:

provider

	<provider android:authorities="com.facebook.app.FacebookContentProvider{APP_ID}"
          android:name="com.facebook.FacebookContentProvider"
          android:exported="true"/>

以上详细内容, 见 [Android - Getting Started][1].


# 分享到微信


[Android微信朋友圈、微信分享回调函数没有响应][2]

最近在开发Android应用的微信朋友圈、微信分享，在开发过程中发现回调函数一直没有响应，后来发现一个非常蛋疼的问题。

就是你新建的activity名称一定要是WXEntryActivity，而且一定要放在你申请的时候填写的包名+wxapi下，而且这个activity在AndroidManifest.xml下还要设置android:exported=”true”，呵呵，真蛋碎。

如：

	<activity android:name=”com.xxx.xxx.xxx.wxapi.WXEntryActivity” android:screenOrientation=”portrait”
	android:configChanges=”keyboardHidden|keyboard” android:exported=”true”/>



refs:
[Facebook share on Android](https://developers.facebook.com/docs/sharing/android)  






[1]: https://developers.facebook.com/docs/android/getting-started
[2]: http://www.chenwg.com/android/android%E5%BE%AE%E4%BF%A1%E6%9C%8B%E5%8F%8B%E5%9C%88%E3%80%81%E5%BE%AE%E4%BF%A1%E5%88%86%E4%BA%AB%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0%E6%B2%A1%E6%9C%89%E5%93%8D%E5%BA%94.html

