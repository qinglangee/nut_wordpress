# docker 中运行 gitlab

## 安装 docker
按下不表

## 下载安装一步进行

	sudo docker run --detach \
	    --hostname gitlab.insqt.com \
	    --publish 443:443 --publish 80:80 --publish 22:22 \
	    --name gitlab \
	    --restart always \
	    --volume /srv/gitlab/config:/etc/gitlab \
	    --volume /srv/gitlab/logs:/var/log/gitlab \
	    --volume /srv/gitlab/data:/var/opt/gitlab \
	    gitlab/gitlab-ce:latest
启动成功的话可以能过 `http://localhost/` 访问， 默认用户名密码是

	username: `root`
	password: `5iveL!fe`
修改配置文件，设置external_url ，这会影响project的 ssh 或 https 的前缀。修改方式见下面的[配置Gitlab][]  
不设置 external_url 时， 默认使用 `--hostname gitlab.abc.com` 传入的 hostname
*对于docker 中的 gitlab, ssh 方式访问时， 前面需要加 `ssh://` 前缀, 端口映射了的话，后面也要加上 `22` 端口映射到的端口。*

	ssh://git@gitlab.insqt.com:3344/g1/pp1.git
*修改映射的端口， 如果22，80，443等被占用了，映射到主机的闲置端口*
iptables 服务重启后docker也需要重启，docker 服务启动时会创建需要的iptables 规则

	docker run --detach \
	    --hostname gitlab.insqt.com \
	    --publish 3343:443 --publish 3345:80 --publish 3344:22 \
	    --name gitlab \
	    --restart always \
	    --volume /srv/gitlab/config:/etc/gitlab \
	    --volume /srv/gitlab/logs:/var/log/gitlab \
	    --volume /srv/gitlab/data:/var/opt/gitlab \
	    gitlab/gitlab-ce:latest
*在开始时就传入env配置参数* （这种方式需要每次重新创建时都带上这些参数）

	docker run --detach \
	    --hostname gitlab.insqt.com \
	    --env GITLAB_OMNIBUS_CONFIG="external_url 'http://gitlab.insqt.com/'; gitlab_rails['lfs_enabled'] = true;" \
	    --publish 3343:443 --publish 3345:80 --publish 3344:22 \
	    --name gitlab \
	    --restart always \
	    --volume /srv/gitlab/config:/etc/gitlab \
	    --volume /srv/gitlab/logs:/var/log/gitlab \
	    --volume /srv/gitlab/data:/var/opt/gitlab \
	    gitlab/gitlab-ce:latest
持久化数据的保存

Local location	   		Container location	 Usage
/srv/gitlab/data		/var/opt/gitlab	     For storing application data
/srv/gitlab/logs		/var/log/gitlab	     For storing logs
/srv/gitlab/config		/etc/gitlab	         For storing the GitLab configuration files
## 配置 Gitlab 
方式一： 建立连接到容器的一个会话

	sudo docker exec -it gitlab /bin/bash
方式二：直接编辑文件

	sudo docker exec -it gitlab vi /etc/gitlab/gitlab.rb
设置完成后重启容器

	sudo docker restart gitlab
设置内容

	external_url 'http://gitlab.insqt.com'  # 链接前缀， 这个值只在显示 git 的 ssh 或 https 链接时起作用， 创建 group 或 project 时显示的不是这个值
其它一些相关配置  
[SMTP settings](http://docs.gitlab.com/omnibus/settings/smtp.html)  
[Enabling HTTPS](http://docs.gitlab.com/omnibus/settings/nginx.md#enable-https)  
## 更新 Gitlab image

停止运行的容器:

	sudo docker stop gitlab
删除容器:

	sudo docker rm gitlab
摘取新的image:

	sudo docker pull gitlab/gitlab-ce:latest
在原先的配置基础上再次创建容器：

	sudo docker run --detach \
	--hostname gitlab.example.com \
	--publish 443:443 --publish 80:80 --publish 22:22 \
	--name gitlab \
	--restart always \
	--volume /srv/gitlab/config:/etc/gitlab \
	--volume /srv/gitlab/logs:/var/log/gitlab \
	--volume /srv/gitlab/data:/var/opt/gitlab \
	gitlab/gitlab-ce:latest
在第一次运行时， Gitlab 会重新配置和更新自己。

refs:  
[The official GitLab Community Edition Docker image](https://hub.docker.com/r/gitlab/gitlab-ce/)  
[GitLab Documentation](http://docs.gitlab.com/omnibus/docker/)  
