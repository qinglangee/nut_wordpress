# linux /usr/bin/ld cannot find 解决 
问题：
在linux环境编译应用程式或lib的source code时常常会出现如下的错误讯息：

        /usr/bin/ld: cannot find -lxxx 
这些讯息会随着编译不同类型的source code 而有不同的结果出来如：

        /usr/bin/ld: cannot find -lc
        /usr/bin/ld: cannot find -lltdl
        /usr/bin/ld: cannot find -lXtst 

其中xxx即表示函式库文件名称，如上例的：libc.so、libltdl.so、libXtst.so。
其命名规则是：lib+库名(即xxx)+.so。

会发生这样的原因有以下三种情形：

    1 系统没有安装相对应的lib
    2 相对应的lib版本不对
    3 lib(.so档)的symbolic link 不正确，没有连结到正确的函式库文件(.so)

对于上述三种原因有一篇文章写的很棒可参考这一篇文章的第４点： [gcc命令祥解][1]


解决方法：
(1)先判断在/usr/lib 下的相对应的函式库文件(.so) 的symbolic link 是否正确．若不正确改成正确的连结目标即可解决问题。

(2)若不是symbolic link 的问题引起，而是系统缺少相对应的lib安装lib即可解决。

(3)如何安装缺少的lib：
以上面三个错误讯息为例：

    错误1缺少libc的LIB
    错误2缺少libltdl的LIB
    错误3缺少libXtst的LIB 

　

　 以Ubuntu为例：
　　先搜寻相对应的LIB再进行安装的作业如：

    apt-cache search libc-dev
    apt-cache search libltdl-dev 
    apt-cache search libXtst-dev


实例：
在进行输入法gcin的Source Code的编译时出现以下的错误讯息：

    /usr/bin/ld: cannot find -lXtst


经检查后发现是：
lib(.so档)的symbolic link 不正确

解决方法如下：

    cd /usr/lib
    ln -s libXtst.so.6 libXtst.so


如果在/usr/lib的目录下找不到libXtst.so 档，那么就表示系统没有安装libXtst的函式库。
解法如下：

    apt-get install libxtst-dev

 

 

环境：vmware server + RHEL5.4 +fcitx3.63在执行make时遇到错误

	[root@localhost  fcitx-3.6.3] make

	make  all-recursive
	make[1]: Entering directory `/home/oracle/Desktop/fcitx-3.6.3'
	Making all in doc
	make[2]: Entering directory `/home/oracle/Desktop/fcitx-3.6.3/doc'
	make[2]: Nothing to be done for `all'.
	make[2]: Leaving directory `/home/oracle/Desktop/fcitx-3.6.3/doc'
	Making all in xpm
	make[2]: Entering directory `/home/oracle/Desktop/fcitx-3.6.3/xpm'
	make[2]: Nothing to be done for `all'.
	make[2]: Leaving directory `/home/oracle/Desktop/fcitx-3.6.3/xpm'
	Making all in lib
	make[2]: Entering directory `/home/oracle/Desktop/fcitx-3.6.3/lib'
	make[2]: Nothing to be done for `all'.
	make[2]: Leaving directory `/home/oracle/Desktop/fcitx-3.6.3/lib'
	Making all in src
	make[2]: Entering directory `/home/oracle/Desktop/fcitx-3.6.3/src'
	gcc -O2 -fno-strength-reduce -g -O2   -D_ENABLE_TRAY    -Wall -lXpm -lXtst -lpthread  -o fcitx IC.o ime.o InputWindow.o KeyList.o main.o MainWindow.o MyErrorsHandlers.o punc.o py.o PYFA.o pyMapTable.o pyParser.o sp.o tools.o ui.o table.o xim.o qw.o tray.o TrayWindow.o DBus.o vk.o about.o QuickPhrase.o AutoEng.o extra.o internalVersion.o ImeRemote.o ../lib/libXimd.a -lX11
	/usr/bin/ld: cannot find -lXtst
	collect2: ld returned 1 exit status
	make[2]: *** [fcitx] Error 1
	make[2]: Leaving directory `/home/oracle/Desktop/fcitx-3.6.3/src'
	make[1]: *** [all-recursive] Error 1
	make[1]: Leaving directory `/home/oracle/Desktop/fcitx-3.6.3'
	make: *** [all] Error 2

经过检查在目录  /usr/bin/ld下面没有发现lXtst

refs:  
[linux /usr/bin/ld cannot find 解决 ](http://blog.csdn.net/mzwang123/article/details/6702889)  
[gcc命令详解][1]  


[1]: http://blog.csdn.net/dqmengxiang/article/details/5864149