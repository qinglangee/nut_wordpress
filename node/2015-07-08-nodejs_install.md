# nodejs 安装

## 二进制安装

[下载页面][1]里下载一个　Linux 二进制包, 解压就行了．　bin 目录添加到 path 中．  
或者链接一下：

	ln -s /home/zhch/software/node-v0.12.6-linux-x64/bin/node /usr/local/bin/node
	ln -s /home/zhch/software/node-v0.12.6-linux-x64/bin/npm /usr/local/bin/npm

## 源码安装

[下载页面][1]里下载源码包，解压

	./configure
	make
	make install 
搞定






[1]: https://nodejs.org/download/