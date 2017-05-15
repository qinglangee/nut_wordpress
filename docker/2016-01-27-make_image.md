# docker 制作镜像

## 在 centos 系统上制作 centos 镜像 
[Docker 从零开始制作基础镜像[centos]][1]
[官方教程][2]  
[制作脚本][3]  

这个应该是复制系统的文件，然后安装其它包.

执行命令

	chmod +x mkimage-yum.sh
	./mkimage-yum.sh  centos7    # 参数是名字，可以根据实际版本取名字
名字还有限制，最后因为名字失败太悲催了 *repository name component must match `"[a-z0-9](?:-*[a-z0-9])*(?:[._][a-z0-9](?:-*[a-z0-9])*)*"`*

成功结束后， 可以用 `docker images` 查看。





[1]: http://www.cnblogs.com/2018/p/4633940.html
[2]: https://docs.docker.com/engine/articles/baseimages/
[3]: https://github.com/docker/docker/blob/master/contrib/mkimage-yum.sh