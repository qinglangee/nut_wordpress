# 设置android sdk使用代理

## for linux

解决方法是先建好代理, 然后创建文件 ~/.android/androidtool.cfg 让android使用代理

	### Settings for Android Tool
	#Tue Jun 12 01:34:55 PDT 2012
	http.proxyPort=3128
	sdkman.monitor.density=108
	http.proxyHost=127.0.0.1
	sdkman.show.update.only=true
	sdkman.ask.adb.restart=false
	sdkman.force.http=true
	sdkman.show.updateonly=true

这个文件可以已经存在了, 像下面这样子:

	http.proxyPort=
	http.proxyHost=127.0.0.1\:3128

这个在我这不管用, 改成下面这样就可以了:

	http.proxyPort=3128
	http.proxyHost=127.0.0.1

*不过挂http代理是不能翻墙的,所以还是得VPN*


refs:  
[Android SDK Manager Proxy Settings in LINUX][1]  


[1]: http://stackoverflow.com/questions/10634202/android-sdk-manager-proxy-settings-in-linux