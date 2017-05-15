# docker 基础知识

## [下载][1]一个镜像 

	$ sudo docker pull ubuntu:12.04
	# 相当于从官方网站下载
	$ sudo docker pull registry.hub.docker.com/ubuntu:12.04
	# 非官方的镜像需要指定全路径
	$ sudo docker pull dl.dockerpool.com:5000/ubuntu:12.04
使用镜像创建一个容器， 运行其中的 bash

	$ sudo docker run -t -i ubuntu:12.04 /bin/bash
使用 `docker images` 显示本地已有的镜像。

## [创建一个镜像][2]  
### 1. 修改现有的镜像 

命令：

	# 运行一个镜像，注意：记住容器的 ID，稍后还会用到。
	$ sudo docker run -t -i training/sinatra /bin/bash
	root@0b2616b0e5a8:/#

	# 修改内容 ， 在容器中添加 json 和 gem 两个应用。
	root@0b2616b0e5a8:/# gem install json
 
	# 当结束后，我们使用 exit 来退出，现在我们的容器已经被我们改变了，使用 docker commit 命令来提交更新后的副本。
	$ sudo docker commit -m "Added json gem" -a "Docker Newbee" 0b2616b0e5a8 ouruser/sinatra:v2  
	4f177bd27a9ff0f6dc2a830403925b5360bfe0b93d476f7fc3231110e7f71b1c
其中，-m 来指定提交的说明信息，跟我们使用的版本控制工具一样；-a 可以指定更新的用户信息；之后是用来创建镜像的容器的 ID；最后指定目标镜像的仓库名和 tag 信息。创建成功后会返回这个镜像的 ID 信息。

### 2. 利用 Dockerfile 来创建镜像

新建一个目录和一个 Dockerfile

	$ mkdir sinatra
	$ cd sinatra
	$ touch Dockerfile

Dockerfile 中每一条指令都创建镜像的一层，例如：

	# This is a comment
	FROM ubuntu:14.04
	MAINTAINER Docker Newbee <newbee@docker.com>
	RUN apt-get -qq update
	RUN apt-get -qqy install ruby ruby-dev
	RUN gem install sinatra
Dockerfile 基本的语法是

1. 使用#来注释
2. FROM 指令告诉 Docker 使用哪个镜像作为基础
3. 接着是维护者的信息
4. RUN开头的指令会在创建中运行，比如安装一个软件包，在这里使用 apt-get 来安装了一些软件

编写完成 Dockerfile 后可以使用 docker build 来生成镜像。

	$ sudo docker build -t="ouruser/sinatra:v2" .
其中 -t 标记来添加 tag，指定新的镜像的用户信息。 “.” 是 Dockerfile 所在的路径（当前目录），也可以替换为一个具体的 Dockerfile 的路径。
*注意一个镜像不能超过 127 层*
此外，还可以利用 ADD 命令复制本地文件到镜像；用 EXPOSE 命令来向外部开放端口；用 CMD 命令来描述容器启动后运行的程序等。例如

	# put my local web site in myApp folder to /var/www
	# 这条命令是把 myApp 目录下的内容放到 /var/www目录下
	ADD myApp /var/www
	# expose httpd port
	EXPOSE 80
	# the command to run
	CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

现在可以利用新创建的镜像来启动一个容器。

	$ sudo docker run -t -i ouruser/sinatra:v2 /bin/bash
	root@8196968dac35:/#
还可以用 docker tag 命令来修改镜像的标签（是添加了一个标签吧）。

	$ sudo docker tag 5db5f8471261 ouruser/sinatra:devel
## [导出和载入镜像][3]
导出镜像， 保存到文件中

	$ sudo docker images
	REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
	ubuntu              14.04               c4ff7513909d        5 weeks ago         225.4 MB
	...
	$sudo docker save -o ubuntu_14.04.tar ubuntu:14.04

载入镜像
可以使用 docker load 从导出的本地文件中再导入到本地镜像库，例如

	$ sudo docker load --input ubuntu_14.04.tar
或

	$ sudo docker load < ubuntu_14.04.tar
## 删除镜像
如果要移除本地的镜像，可以使用 `docker rmi` 命令。注意 `docker rm` 命令是移除容器。

	$ sudo docker rmi training/sinatra
*注意：在删除镜像之前要先用 docker rm 删掉依赖于这个镜像的所有容器。*

## [启动容器][4]

下面的命令则启动一个 bash 终端，允许用户进行交互。

	$ sudo docker run -t -i ubuntu:14.04 /bin/bash
	root@af8bae53bdd3:/#

其中，-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上， -i 则让容器的标准输入保持打开

启动已终止容器
可以利用 `docker start` 命令，直接将一个已经终止的容器启动运行。

指定名字启动容器

	docker run -d -P --name web training/webapp python app.py
后台启动，指定端口(前面是主机端口，后面是容器端口) 

	docker run -d -p 7080:8080 --name tomcat tomcat-centos7 bash


要让 Docker 容器在后台以守护态（Daemonized）形式运行。此时，可以通过添加 -d 参数来实现。

	$ sudo docker run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
	1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147

容器启动后会返回一个唯一的 id，也可以通过 docker ps 命令来查看容器信息。

	$ sudo docker ps
	CONTAINER ID  IMAGE         COMMAND               CREATED        STATUS       PORTS NAMES
	1e5535038e28  ubuntu:14.04  /bin/sh -c 'while tr  2 minutes ago  Up 1 minute        insane_babbage

要获取容器的输出信息，可以通过 docker logs 命令。

	$ sudo docker logs insane_babbage
可以使用 `docker stop "container id" ` 来终止一个运行中的容器。
终止状态的容器可以用 `docker ps -a` 命令看到。
处于终止状态的容器，可以通过 `docker start` 命令来重新启动。
此外，`docker restart` 命令会将一个运行态的容器终止，然后再重新启动它。


## [进入容器][5]
进入容器

	$ docker attach docker_name
## 删除容器

	docker rm  container_name
清理后台所有停止的容器

	docker ps -a -q | xargs docker rm


## [数据卷][6]
数据卷是一个可供一个或多个容器使用的特殊目录，它绕过 UFS，可以提供很多有用的特性：

1. 数据卷可以在容器之间共享和重用
2. 对数据卷的修改会立马生效
3. 对数据卷的更新，不会影响镜像
4. 卷会一直存在，直到没有容器使用

在用 docker run 命令的时候，使用 -v 标记来创建一个数据卷并挂载到容器里。在一次 run 中多次使用可以挂载多个数据卷
下面创建一个 web 容器，并加载一个数据卷到容器的 /webapp 目录。

	$ sudo docker run -d -P --name web -v /webapp training/webapp python app.py
	$ sudo docker run -d -P --name web -v /webapp -v /abcd -v /def training/webapp python app.py  # 多次创建多个数据卷
使用 -v 标记也可以指定挂载一个本地主机的目录到容器中去。(主机目录:容器目录)

	$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
Docker 挂载数据卷的默认权限是读写，用户也可以通过 :ro 指定为只读。

	$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp:ro training/webapp python app.py
### 容器挂载目录
1. 是挂载到容器中已有目录还是不存在的目录？
*已存在的，不存在的都可以*
2. 如果是已有目录，目录中有内容可不可以挂载？
*可以挂载，原来目录会被挂载的目录替换掉*












[1]: http://dockerpool.com/static/books/docker_practice/image/pull.html
[2]: http://dockerpool.com/static/books/docker_practice/image/create.html  
[3]: http://dockerpool.com/static/books/docker_practice/image/save_load.html  
[4]: http://dockerpool.com/static/books/docker_practice/container/run.html  
[5]: http://dockerpool.com/static/books/docker_practice/container/enter.html
[6]: dockerpool.com/static/books/docker_practice/data_management/volume.html