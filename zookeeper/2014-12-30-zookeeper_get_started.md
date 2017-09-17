# zookeeper 入门
下载一份[zookeeper][2], 解压后在 docs 目录中有帮助文档
## 单实例操作

1. 建立一个配置文件  conf/zoo.cfg:
```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
```
2. 启动 `bin/zkServer.sh  start`
	

# 命令
[Getting Started][1]

## 配置
conf/zoo.cfg:

tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
## 启动
bin/zkServer.sh start

## 连接到服务器
bin/zkCli.sh -server 127.0.0.1:2181

## 增删改查
help
ls /
create /zktest mydata
ls /
get /zktest
set /zktest
delete /zktest









# links

[Getting Started][1]  

[1]: http://zookeeper.apache.org/doc/trunk/zookeeperStarted.html#sc_InstallingSingleMode
[2]: http://zookeeper.apache.org/releases.html