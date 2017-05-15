# adb 不能识别设备的解决方法

## adb devices 不显示设备
在adb_usb.ini 中添加厂商ID

	echo "0x2717" >> ~/.android/adb_usb.ini   #  小米2
	echo "0x29a9" >> ~/.android/adb_usb.ini   #  锤子 T1

如何查看 厂商ID, 先连上手机执行 `lsusb`, 再拔下手机执行一遍, 看看哪个消失了就是.  
例如下面的命令, ID 29a9:701b,  29a9就是厂商ID

	lsusb
>Bus 002 Device 019: ID 29a9:701b  
Bus 002 Device 004: ID 046d:c05a Logitech, Inc. M90/M100 Optical Mouse
Bus 002 Device 005: ID 04b3:301b IBM Corp. SK-8815 Keyboard
Bus 002 Device 003: ID 04b3:301a IBM Corp. 
Bus 002 Device 002: ID 8087:0020 Intel Corp. Integrated Rate Matching Hub


在用户的 home 目录下，寻找 .android 目录，如果没有就创建。在 .android 目录下新建一个文件，叫`adb_usb.ini`；添加前面获得的 VID值  0x2717　 到 `adb_usb.ini` 中，在 shell 中 分别输入 adb kill-server, adb start-server, adb devices；若能看到 devices 列出，那么就成功了，之后就可以使用eclipse运行应用开发了.
## adb devices 显示没权限

> adb devices
List of devices attached 
????????????	no permissions

这里用一下上面查出的ID , Bus 002 Device 019: ID 29a9:701b  
在 `/etc/udev/rules.d` 下创建一个配置文件 

	sudo vim /etc/udev/rules.d/50-android.rules
加入以下内容：

    SUBSYSTEM=="usb", ATTRS{idVendor}=="0bb4", ATTRS{idProduct}=="0c87",MODE="0666"
    SUBSYSTEM=="usb", SYSFS{idVendor}=="29a9", MODE="0666"     # ATTRS{idProduct} 可以不需要
    SUBSYSTEM=="usb", SYSFS{idVendor}=="2717", MODE="0666"     
idVendor  和 idProduct 分别就是 ID 29a9:701b  冒号前后的数字,  

	sudo chmod a+rx /etc/udev/rules.d/50-android.rules
	sudo restart udev  # 这句没执行好像也可以, 可能后面的命令执行了
然后关掉adb, `adb kill-server`, 并 *用sudo启动*, `sudo adb start-server`,  这里一定要用sudo 启动才能正常识别到device.  
(*很重要*)拔掉usb重新连上再执行：

	adb kill-server    # 记得看一下关掉了没, 有设备连着时可能没关掉
	sudo adb start-server

refs:  
[原创干货：锤子如何连接MacOS系统调试][1]   
[ubuntu下adb不识别小米2][2]  
[Ubuntu adb devices : no permissions 解决方法 ][3]  
[官方文档][4]  
[Linux下Android ADB驱动安装详解 ][5]  




[1]: http://bbs.smartisan.cn/forum.php?mod=viewthread&tid=60812
[2]: http://blog.sina.com.cn/s/blog_6f7af91301018wpe.html
[3]: http://blog.csdn.net/chychc/article/details/7276294
[4]: http://developer.android.com/tools/device.html
[5]: http://blog.csdn.net/zhenwenxian/article/details/5901350