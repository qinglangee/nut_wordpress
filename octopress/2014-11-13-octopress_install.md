# octopress 安装
git clone

	git clone git://github.com/imathis/octopress.git octopress
	cd octopress
Next, install dependencies.

	gem install bundler   # 需要 sudo
	###rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
	bundle install       # 需要 sudo 的权限
	
	#Install the default Octopress theme.
	rake install
 到这儿, octopress就算是安装好了. 
*按照 jeklly 方式启动就好了, jekyll serve方式只能本机访问, rake preview方式可以外部访问, 原因暂不清楚*

## 安装主题
安装一个[Octoplate][1]主题,

    $ cd octopress
    $ git clone git://github.com/mjhea0/octoplate.git .themes/octoplate
    $ rake "install[octoplate]"
    $ rake generate && rake preview
    $ rake deploy

新添加的Theme被放到octopress根目录下的.theme文件夹，执行rake install,能够将主题包中的内容加载到octopress根目录下，并提换已有文件。

*注：Octoplate主题包中本身缺少一些文件，因而最好在原有Theme为classic的前提下进行添加该Theme的操作。*



refs:  
[Octopress Setup](http://octopress.org/docs/setup/)  
[Octopress 主题美化 ](http://lzteng.com/Technology/2014/02/04/octopress-beautification/)  


[1](https://github.com/mjhea0/octoplate)  