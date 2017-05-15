# tensorFlow　初步

## 安装

### Ubuntu pip 安装
安装　pip 工具　`sudo apt-get install python-pip python-dev`
设置安装URL `export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.9.0-cp27-none-linux_x86_64.whl`
*链接是0.9.0版本的，可以自行找其它版本的链接*
安装　`sudo pip install --upgrade $TF_BINARY_URL`

### 用　Docker 安装
可以去才云科技看一下，找相关的Docker 镜像．Google　自己也提供各个版本的镜像．

### 源码编译安装
编译安装需要先安装一些依赖工具
编译工具　　Bazel -> Java8 , 还有其它各种等等，就先不装了．
