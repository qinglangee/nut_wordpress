# adb 使用错误

## adb server version (36) doesn't match this client (39); killing...
把Genymotion的ADB换成系统的就行了。

网上有两种情况：
1. [Genymotion 使用了自已的 adb tools, 与命令行中的不一致][1]   
2. [也有可能是adb路径与 Android Studio中的 Android SDK 路径不一致][2]    

[1]: http://stackoverflow.com/questions/38214012/appium-adb-server-version-31-doesnt-match-this-client-36
[2]: http://stackoverflow.com/questions/43050370/adb-server-version-36-doesnt-match-this-client-39-not-using-genymotion/43080159#43080159