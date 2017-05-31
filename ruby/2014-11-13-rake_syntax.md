# rake 语法
Rakefile、rakefile、RakeFile.rb和rakefile.rb

	# 设置默认任务
	task :default => [:today]

	# 调用别的任务
	desc "今天的任务"
	task :today do
	Rake::Task["home:cook"].invoke
	Rake::Task["home:laundry"].invoke
	end

	namespace :home do
		desc "任务1 -- 买菜"
		task :purchaseVegetables do
		puts "到沃尔玛去买菜。"
		end

		# 依赖别的任务 
		desc "任务2 -- 做饭"
		task :cook => :purchaseVegetables do
		puts "做一顿香喷喷的饭菜。"
		end

		desc "任务3 -- 洗衣服"
		task :laundry do
		puts "把所有衣服扔进洗衣机。"
		end
	end

传参数  , [Tasks with Arguments][1]

	task :my_task, [:arg1, :arg2] do |t, args|
	  puts "Args were: #{args}"
	end

	task :invoke_my_task do
	  Rake.application.invoke_task("my_task[1, 2]")
	end

	# or if you prefer this syntax...
	task :invoke_my_task_2 do
	  Rake::Task[:my_task].invoke(3, 4)
	end
命令行调用 

	rake "my_task[arg1, arg2]"
## 命名空间

	namespace :home do
	...
	end
运行时用 `rake home:cook`

## 错误信息

如果报错如下 :  开头加上 encoding
>invalid multibyte char (US-ASCII)

	#encoding: utf-8





refs:  
[Ruby的头号Gem：Rake ](http://blog.csdn.net/smilewater/article/details/1683808)  
[Rakefile Format](https://github.com/jimweirich/rake/blob/master/doc/rakefile.rdoc)  
[Rake中传参数](http://stackoverflow.com/questions/825748/how-do-i-pass-command-line-arguments-to-a-rake-task)  
[rails invalid multibyte char](http://richfisher.blog.163.com/blog/static/178245387201135105430964/)  



[1]: https://github.com/jimweirich/rake/blob/master/doc/rakefile.rdoc#tasks-with-arguments