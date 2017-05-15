# docker startup

Get Started with Docker for [Windows][1]
This is written for users of Windows. If you are not using Windows, see the Linux or Mac OS X version.

This getting started is for non-technical users who are interested in learning about Docker. By following this getting started, you’ll learn fundamental Docker features by performing some simple tasks. You’ll learn how to:

    install Docker
    run a software image in a container
    browse for an image on Docker Hub
    create your own image and run it in a container
    create a Docker Hub account and an image repository
    create an image of your own
    push your image to Docker Hub for others to use

The getting started was user tested to reduce the chance of users having problems. For the best chance of success, follow the steps as written the first time before exploring on your own. It takes approximately 45 minutes to complete.
Make sure you understand…

This getting started uses Docker commands with a terminal window. You don’t need to be experienced using a command line, but you should be familiar with how to open one and type commands.

Go to the next page to install.

## Learn about images & containers
container 是一个基本功能的 Linux 系统
image 是加载到 container 中运行的软件。根据构建方式的不同， 一个 image 可能只是运行一条命令然后退出， hello-world 就是这样的。

## Find and run the whalesay image
1.在 [Docker Hub](https://hub.docker.com/)  可以搜索， 输入 whalesay 搜索，得到列表。 在结果中点击 `docker/whalesay`, 可以查看相关信息。 包括这个 image 用了什么软件，怎么使用等等。
2.`docker run docker/whalesay cowsay boo` 下载并运行 whalesay.
3.使用`docker images`命令显示本机的 images.

## Build your own image

###　Step 1: Write a Dockerfile
创建一个目录放你的 Docker Build, 进入目录创建 Dockerfile 文件并编辑
Dockerfile：

	FROM docker/whalesay:latest
	RUN apt-get -y update && apt-get install -y fortunes
	CMD /usr/games/fortune -a | cowsay



`FROM` 关键字告诉 Docker 你的 image 是基于哪一个 image. docker/whalesay 已经包含了 cowsay 程序， 就以它为基础。
`fortunes` 会打印一个名言警句，先安装这个程序。
最后一个`CMD`让 fortune 的输出输入到 cowsay.

###　Step 2: Build an image from your Dockerfile


	docker build -t docker-whale .
这个命令根据当前目录的 Dockerfile 文件在你的本地机器上构建一个 docker-whale 的 image.

### 运行一下

	docker run docker-whale

## Create a Docker Hub account & repository
自己创建帐号就好了， 网址是 https://hub.docker.com

## Tag, push, and pull your image

### Step 1: Tag and push the image
`docker images` 查看新创建的 image 的 ID

>$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
docker-whale        latest              35b0b4c57300        17 minutes ago      255.5 MB
hello-world         latest              975b84d108f1        3 months ago        960 B
docker/whalesay     latest              fb434121fc77        8 months ago        247 MB

先把 image 与 namespace 关联起来， namespace 就是你的用户名，

	docker tag 35b0b4c57300 maryatdocker/docker-whale:latest
命令行登录 docker hub

	docker login --username=yourhubusername --email=youremail@company.com
推送 image

	docker push maryatdocker/docker-whale
###　Step 2: Pull your new image
先移除本地 repository, 可以用名字，也可以用 ID

	$ docker rmi -f 7d9495d03763
	$ docker rmi -f docker-whale
然后重新拉取下来

	docker pull yourusername/docker-whale


refs:  

[1]: https://docs.docker.com/windows/