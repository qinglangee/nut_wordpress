# ubuntu 运行中缺少 lib 的错误

./jd-gui: error while loading shared libraries: libgtk-x11-2.0.so.0: cannot open shared object file: No such file or directory

	sudo apt-get install ia32-libs-gtk
Now run the application again and the error should go away. see [source1][1], [source2 article][2]   
如果是ubuntu 14.04，则请先执行：
方法1：

	sudo gedit /etc/apt/sources.list
	然后在最后添加上： deb http://archive.ubuntu.com/ubuntu/ raring main restricted universe multiverse




refs:  

[fix-error-while-loading-shared-libraries-libgtk-x11-2-0-so-0][2]  




[1]: http://blog.csdn.net/michaelpp/article/details/8904300
[2]: http://www.techmaze.net/fix-error-while-loading-shared-libraries-libgtk-x11-2-0-so-0/