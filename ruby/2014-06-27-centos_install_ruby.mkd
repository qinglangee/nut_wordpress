# centos 安装 ruby

到 ftp://ftp.ruby-lang.org/pub/ruby 找到最新版本

	$ wget ftp://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-p180.tar.gz
	$ tar xzvf ruby-1.9.2-p180.tar.gz
	$ cd ruby-1.9.2-p180
	$ ./configure && make
	$ sudo make install
*后来gem安装jekyll出错了, 就用rvm又重新装了个1.9.3版本的*


# gem 安装出错

	ERROR:  Loading command: install (LoadError)
	    no such file to load -- zlib
	ERROR:  While executing gem ... (NameError)
	    uninitialized constant Gem::Commands::InstallCommand

解决办法是：

进入ruby源码文件夹 
安装ruby自身提供的zlib包 

	#cd ext/zlib
	#ruby ./extconf.rb
	#make
	#make install