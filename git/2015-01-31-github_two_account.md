# 如何在同一台电脑上使用两个github账户

场景：使用github的时候，大家都知道需要给该账号添加一个SSH key才能访问，参考具体设置。当然如果你在多台机器使用一个账户，你可以为该账户添加多个SSH key。由于github是使用SSH key的fingerprint来判定你是哪个账户，而不是通过用户名，这样你就可以在设置完之后，在本地直接执行下面的语句，它就会自动使用你的.ssh/id_rsa.pub所对应的账户进行登陆，然后执行相关命令。

	#本地建库
	$ git init
	$ git commit -am "first commit'

	#push到github上去
	$ git remote add origin git@github.com:xxxx/test.git
	$ git push origin master
但是如果你想在一台机器使用两个github账号（比如私人账号和工作用账号）。这个时候怎么指定push到哪个账号的test仓库上去呢？

解决方案（假设你已经拥有私有账号且已经OK，现在想使用另一个工作用账号）：

1 为工作账号生成SSH Key

		#存储key的时候，不要覆盖现有的id_rsa，使用一个新的名字，比如id_rsa_work
		$ ssh-keygen -t rsa -C "your-email-address"     # -C 是comment, 添加注释
2 把 *id_rsa_work.pub* 加到你的work账号上
3 把该key加到ssh agent上。由于不是使用默认的.ssh/id_rsa，所以你需要显式告诉ssh agent你的新key的位置

	$ ssh-add ~/.ssh/id_rsa_work    # 可以通过ssh-add -l来确认结果(如果有指纹一样的, 会有问题的, 用keygen时修改一下 comment)
4 配置.ssh/config

	$ vi .ssh/config

	# 加上以下内容
	#default github, 这块不能加, 要不就循环了, 默认的就让它找默认文件就行了
	#Host github.com
	#  HostName github.com
	#  IdentityFile ~/.ssh/id_rsa

	Host github_work
	  HostName github.com
	  IdentityFile ~/.ssh/id_rsa_work
5 这样的话，你就可以通过使用github.com别名 *github_work* 来明确说你要是使用 *id_rsa_work* 的SSH key来连接github，即使用工作账号进行操作。

	#本地建库
	$ git init
	$ git commit -am "first commit'
	 
	#push到github上去
	$ git remote add origin git@github_work:xxxx/test.git
	$ git push origin master
*注意:换了机器后不能用同一个key, 要重新生成一个.  特别注意: 加key的时候要加对仓库啊, 加到别的帐号了再测也没有用啊, 说多了都是泪*
6 验证public key是否匹配了正确的帐号
## 其它

ssh 调试

	ssh -v git@github.com
git 调试

	$ GIT_TRACE=true
	$ export GIT_TRACE
	$ git push origin master
测试 public key 在 github 上被哪个帐号用过了

	ssh -T -ai ~/.ssh/qinglang163 git@github.com


ps: 如果执行ssh-add的时候，出现这样的错误，说明ssh-agent没有启动起来

- Could not open a connection to your authentication agent.

这个时候需要手动启动ssh-agent：

	exec ssh-agent /bin/bash

也可以直接在.bash_profile里面自动启动，这样就不用每次都手动启动


	SSH_ENV="$HOME/.ssh/environment"

	function start_agent {
	     echo "Initialising new SSH agent..."
	     /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
	     echo succeeded
	     chmod 600 "${SSH_ENV}"
	     . "${SSH_ENV}" > /dev/null
	     /usr/bin/ssh-add;
	}

	# Source SSH settings, if applicable

	if [ -f "${SSH_ENV}" ]; then
	     . "${SSH_ENV}" > /dev/null
	     #ps ${SSH_AGENT_PID} doesn't work under cywgin
	     ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
	         start_agent;
	     }
	else
	     start_agent;
	fi

refs:  
原文: [如何在同一台电脑上使用两个github账户](http://www.cnblogs.com/foxracle/archive/2012/07/20/2599830.html)  
[ssh permission问题终极解答](https://help.github.com/categories/ssh/)  