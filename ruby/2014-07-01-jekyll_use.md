# jekyll quick start

	~ $ gem install jekyll
	~ $ jekyll new myblog
	~ $ cd myblog
	~/myblog $ jekyll serve
	# => Now browse to http://localhost:4000
looks [here][1]

## 默认配置
默认配置文件名是`_config.yml`, `jekyll new myblog` 生成的内容是
```
	# Site settings
	title: Your awesome title
	email: your-email@domain.com
	description: "Write an awesome description for your new site here. You can edit this line in _config.yml. It will appear in your document head meta (for Google search results) and in your feed.xml site description."
	baseurl: ""
	url: "http://yourdomain.com"

	# Build settings
	markdown: kramdown
	permalink: pretty
```
>默认目录是_posts, 只有一层结构, 多层目录中的不识别.  
>文件名必须是 yyyy-MM-dd-filename.mkd格式的, 不带日期的也不识别.  

## 常用命令

	$ jekyll build
	# => 当前目录会被生成到 ./_site

	$ jekyll build --destination <destination>
	# => 当前目录会被生成到 <destination>

	$ jekyll build --source <source> --destination <destination>
	$ jekyll build --watch

	$ jekyll serve
	$ jekyll serve --detach
	$ jekyll serve --watch
	$ jekyll serve --watch  --detach

[1]: http://jekyllrb.com/docs/quickstart/
