# android localhost

Android模拟器（simulator）把它自己作为了localhost,也就是说，代码中使用localhost或者127.0.0.1来访问，都是访问模拟器自己！这是不行的！
如果你想在模拟器simulator上面访问你的电脑，那么就使用android内置的IP 10.0.2.2 吧，10.0.2.2 是模拟器设置的特定ip，是你的电脑的别名alias

记住，在模拟器上用10.0.2.2访问你的电脑本机。

详细请参考Android文档 [android-sdk-windows\docs\guide\developing\devices\emulator.html]()下的Emulator Networking
          
	Network Address 	Description
	10.0.2.1 	Router/gateway address
	10.0.2.2 	Special alias to your host loopback interface (i.e., 127.0.0.1 on your development machine)
	10.0.2.3 	First DNS server
	10.0.2.4 / 10.0.2.5 / 10.0.2.6 	Optional second, third and fourth DNS server (if any)
	10.0.2.15 	The emulated device's own network/ethernet interface
	127.0.0.1 	The emulated device's own loopback interface 