# jekyll 安装

## 安装最新版本啊
1. 按照末尾换成淘宝ruby源
2. `gem install jekyll` 就可以了

## git repo

	$ git clone https://github.com/jekyll/jekyll.git
	$ cd jeklly
	$ gem install jekyll


## gem 安装出错 (原先是编译安装的2.1.2版本ruby)

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
试过后这个方法没起作用

## rvm 重装 ruby
手动安装 ruby后 rvm 在 /usr/local/rvm/bin
参考 [GEM UPDATE –SYSTEM => CANNOT LOAD SUCH FILE — ZLIB][1]

	rvm pkg install zlib
	rvm remove 1.9.3
	rvm install 1.9.3 -C –with-zlib-dir=$rvm_path/usr
结果报错 

	configure: error: invalid variable name: `–with-zlib-dir'
加个横线还是报错

	configure: error: invalid variable name: `–-with-zlib-dir'
把参数全去掉, 不报错了

	rvm install 1.9.3
好, ruby 1.9.3装好了. 再安装jekyll

	$ gem install jekyll
安装了一大串东西, 半道又出错了, 再说吧 , 困死了.

	RDoc::Parser::Ruby failure around line 1 of
	vendor/pygments-main/tests/examplefiles/ruby_func_def.rb

	Before reporting this, could you check that the file you're documenting
	has proper syntax:

	  /usr/local/rvm/rubies/ruby-1.9.3-p547/bin/ruby -c vendor/pygments-main/tests/examplefiles/ruby_func_def.rb

	RDoc is not a full Ruby parser and will fail when fed invalid ruby programs.

	The internal error was:

	        (NoMethodError) undefined method `name' for #<RDoc::RubyToken::TkLPAREN:0x00000003f3da60>

	ERROR:  While executing gem ... (NoMethodError)
	    undefined method `name' for #<RDoc::RubyToken::TkLPAREN:0x00000003f3da60>
*zzzZZZ*
好了, 现在是第二天了, 第二天再执行 `gem install jekyll` 又报另一个错了:

	ERROR:  Could not find a valid gem 'jekyll' (>= 0), here is why:
          Unable to download data from https://rubygems.org/ - Errno::ETIMEDOUT: Connection timed out - connect(2) (https://api.rubygems.org/latest_specs.4.8.gz)
## 换个taobao ruby源试试.

如何使用？

	$ gem sources --remove https://rubygems.org/
	$ gem sources -a https://ruby.taobao.org/
	$ gem sources -l
	*** CURRENT SOURCES ***

	https://ruby.taobao.org
	# 请确保只有 ruby.taobao.org
	$ gem install rails
修改 RVM ，改用本站作为下载源, 提高安装速度。

For Linux

	$ sed -i 's!cache.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
来自[taobao rubyGems镜像][2]
## 换完源再试试

	$ gem install jekyll
	Successfully installed jekyll-2.0.3
	1 gem installed
你妹的, 什么输出也没有, 就这么悄悄地安装成功了!!

参考:
[taobao rubyGems镜像][2]

[1]: https://blog.johncheng.com/2011/11/03/gem-update-system-cannot-load-such-file-zlib/
[2]: http://ruby.taobao.org/