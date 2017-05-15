# linux tesseract 安装

##  centos ([其实文档是针对ubuntu][1])
在centos 中用 `yum search autoconf` 查找相对的包名安装就可以了

* 在centos上安装相对顺利，zlib1g-dev 没装上，也能安装成功 。
* 需要先安装 Leptonica， Leptonica 也是要源码安装， yum 中查不到

Leptonica 安装没什么依赖按顺序来就可以, [下载地址](http://www.leptonica.com/download.html)  

	./configure 
	make && make install
	There's also a 'make check' for testing.


centos tesseract 安装

	sudo yum install autoconf
	yum install automake
	yum install libtool

	yum install libpng-devel
	yum install libjpeg-turbo-devel
	yum install libtiff-devel
	yum install zlib-devel

	yum install libicu-devel     # (if you plan to make the training tools)
	yum install pango-devel      # (if you plan to make the training tools)
	yum install cairo-devel      # (if you plan to make the training tools)

	# 三部分分别合并一下
	yum install autoconf automake libtool
	yum install libpng-devel libjpeg-turbo-devel libtiff-devel zlib-devel
	yum install libicu-devel pango-devel cairo-devel

进入tesseract 源码目录（见下面的 git 下载）

	./autogen.sh
	./configure
	make
	sudo make install
	# 需要先把 tesseract.so 所在目录（一般是/usr/local/lib）添加到 /etc/ld.so.conf 这个配置文件中
	sudo ldconfig      # 重新加载动态库
/etc/ld.so.conf  大约是这个样子

	include ld.so.conf.d/*.conf
	/usr/local/lib
On some systems autotools does not create m4 directory automatically (giving the error: "configure: error: cannot find macro directory 'm4'"). In this case you must create m4 directory (mkdir m4), and then rerun the above commands starting with ./configure.

*If you want the training tools (3.03), you will also need to run the following commands:*

	make training
	sudo make training-install



官方文档
Note: This wiki expects you to be familiar with compiling software on your operation system.

Linux / Other Unices
Dependencies
Autotools
Leptonica
If they are not already installed, you need the following libraries (Ubuntu):

	sudo apt-get install autoconf automake libtool

	sudo apt-get install libpng12-dev
	sudo apt-get install libjpeg62-dev
	sudo apt-get install libtiff4-dev
	sudo apt-get install zlib1g-dev

	sudo apt-get install libicu-dev      # (if you plan to make the training tools)
	sudo apt-get install libpango1.0-dev # (if you plan to make the training tools)
	sudo apt-get install libcairo2-dev   # (if you plan to make the training tools)

You also need to install Leptonica. There is an apt-get package libleptonica-dev, but if you are using an oldish version of Linux, the Leptonica version may be too old, so you will need to build from source.

3.01 requires at least v1.67 of Leptonica.
3.02 requires at least v1.69 of Leptonica. (Both available in Ubuntu 12.04 Precise Pangolin.)
3.03 requires at least v1.70 of Leptonica. (Both available in Ubuntu 14.04 Trusty Tahr.)
The sources are at http://www.leptonica.org/. The instructions at Leptonica README are clear, but basically it is as described in Compilation below.

Ensure that the development headers for Leptonica are installed before compiling Tesseract. Note that if building Leptonica from source, you may need to ensure that /usr/local/lib is in your library path. This is a standard Linux bug, and the information at Stackoverflow is very helpful.

Compilation
Tesseract uses a standard autotools based build system, so the compilation process should be familiar.

	./autogen.sh
	./configure
	make
	sudo make install
	sudo ldconfig
On some systems autotools does not create m4 directory automatically (giving the error: "configure: error: cannot find macro directory 'm4'"). In this case you must create m4 directory (mkdir m4), and then rerun the above commands starting with ./configure.

*If you want the training tools (3.03), you will also need to run the following commands:*

	make training
	sudo make training-install
Build of training tools is not available if you do not have necessary dependencies (pay attention to messages from ./configure script).

Install elsewhere / without root
Tesseract can be configured to install anywhere, which makes it possible to install it without root access.

To install it in $HOME/local:

./autogen.sh
./configure --prefix=$HOME/local/
make install
To install it in $HOME/local using Leptonica libraries also installed in $HOME/local:

./autogen.sh
LIBLEPT_HEADERSDIR=$HOME/local/include ./configure \
  --prefix=$HOME/local/ --with-extra-libraries=$HOME/local/lib
make install
Language Data
Download langugage data file (e.g. 'wget http://tesseract-ocr.googlecode.com/files/tesseract-ocr-3.01.eng.tar.gz' for 3.01 version)
Decompress it ('tar xf tesseract-ocr-3.01.eng.tar.gz')
Move it to installation of tessdata (e.g. 'mv tesseract-ocr/tessdata $TESSDATA_PREFIX' if defined TESSDATA_PREFIX)
You can also use:

export TESSDATA_PREFIX=/some/path/to/tessdata
to point to your tessdata directory (example: if your tessdata path is '/usr/local/share/tessdata' you have to use 'export TESSDATA_PREFIX='/usr/local/share/').




[1]: https://code.google.com/p/tesseract-ocr/wiki/Compiling