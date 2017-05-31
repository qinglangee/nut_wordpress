# gem 安装 RedCloth 时报错

	gem install RedCloth -v '4.2.9'

>ERROR:  Error installing RedCloth:
>	ERROR: Failed to build gem native extension.
>        /usr/bin/ruby1.9.1 extconf.rb
>/usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require': cannot load such file -- mkmf (LoadError)
>	from /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require'
>	from extconf.rb:1:in `<main>'


在 [Stack Overflow][1] 找到答案：mkmf 是 ruby-dev 的一部分，系统未安装。ubuntu下安装：

	sudo apt-get install ruby1.9.1-dev



[1]: http://stackoverflow.com/questions/12731904/rails-installation-failed-on-ubuntu-with-cannot-load-such-file-mkmf