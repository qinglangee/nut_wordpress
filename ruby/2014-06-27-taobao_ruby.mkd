# 换个taobao ruby源试试.

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

来自[taobao rubyGems镜像][1]


[1]: http://ruby.taobao.org/
