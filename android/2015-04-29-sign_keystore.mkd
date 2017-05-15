# android 应用签名

## 生成一个 keystore文件
进入JDK的bin目录

运行如下命令:

	keytool -genkey -alias android.keystore -keyalg RSA -validity 20000 -keystore android.keystore

(-validity 20000代表有效期天数)，命令完成后，bin目录中会生成android.keystore
查看命令

	keytool -list -keystore "android.keystore" 输入你设置的keystore密码



查看 apk签名的脚本

	#!/bin/bash
	mkdir .temp_for_certificate
	cd .temp_for_certificate
	count=0
	while [ -n "$1" ]
	do
	count=$[$count+1]
	echo "(#$count) "`basename "$1"`":"
	echo ""
	path=`jar tf "$1" | grep RSA` #查找apk中RSA文件
	jar xf $1 $path #把RSA文件解压出来
	keytool -printcert -file $path #查看指纹证书
	rm -r $path #删除之前解压的文件
	echo "--------------------------------------------"
	shift
	done
	cd ..
	rm -r .temp_for_certificate 

查看签名也可以使用jarsigner

	jarsigner -verify -verbose -certs Superuser.apk 






## Google -- Signing Your App Manually
You do not need Android Studio to sign your app. You can sign your app from the command line using standard tools from the Android SDK and the JDK. To sign an app in release mode from the command line:

1. Generate a private key using keytool. For example:

use

	$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
This example prompts you for passwords for the keystore and key, and to provide the Distinguished Name fields for your key. It then generates the keystore as a file called my-release-key.keystore. The keystore contains a single key, valid for 10000 days. The alias is a name that you will use later when signing your app.

2. Compile your app in release mode to obtain an unsigned APK.

Sign your app with your private key using jarsigner:

	$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore my_application.apk alias_name
This example prompts you for passwords for the keystore and key. It then modifies the APK in-place to sign it. Note that you can sign an APK multiple times with different keys.

3. Verify that your APK is signed. For example:

use

	$ jarsigner -verify -verbose -certs my_application.apk

4. Align the final APK package using zipalign.

use

	$ zipalign -v 4 your_project_name-unaligned.apk your_project_name.apk
zipalign ensures that all uncompressed data starts with a particular byte alignment relative to the start of the file, which reduces the amount of RAM consumed by an app.




refs:  
[Android app signing](http://developer.android.com/tools/publishing/app-signing.html#signing-manually)  
[Android 生成keystore，两种方式 ](http://blog.csdn.net/ms03001620/article/details/8490314)  
[查看apk签名信息方法](http://www.jb51.net/article/38156.htm)  