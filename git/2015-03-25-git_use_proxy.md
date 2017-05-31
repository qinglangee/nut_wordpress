# git 使用 proxy

写一个脚本, 用netcat作连接转换. 给脚本设置运行权限

	$ cat <<EOF>> ~/bin/git-proxy-wrapper
	#!/bin/sh
	# Put your own values
	PROXY_IP=10.0.0.80
	PROXY_PORT=22000

	nc -x${PROXY_IP}:${PROXY_PORT} -X5 $*

	EOF
	$ chmod +x ~/bin/git-proxy-wrapper
把脚本放到 $PATH 路径中, 设置 git 的环境变量 `GIT_PROXY_COMMAND` 为脚本

	export GIT_PROXY_COMMAND=~/bin/git-proxy-wrapper

再试一次, 是不是可以clone被墙掉的仓库了 ^_^ ,, 没有.... 还是不能 clone!!!






refs:  
[Using git behind a proxy](https://blogs.gnome.org/juanje/2009/07/17/git_behind_proxy/)  
