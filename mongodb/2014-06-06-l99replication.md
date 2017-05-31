#测试机器 
192.168.1.61 192.168.1.64 192.168.1.48  
安装目录  MONGO_HOME = /usr/local/mongodb-linux-x86_64-2.4.10  
数据,日志等其它目录  /data/mongo_2.4.10/  
启动脚本 $MONGO_HOME/start.sh
脚本内容: (replSet 参数的值同一replica set中的每台机器都相同) 

	/usr/local/mongodb-linux-x86_64-2.4.10/bin/mongod --dbpath /data/mongo_2.4.10/data --port 27018 --replSet "rs0"
端口号 27018

# 安装需求
replica set 最好分散放在不同机器上安装, 如果是虚拟机, 应该是host不同的几台虚拟机.  
安装机器之间保证网络通信都没有问题  

# 部署过程

1. 按配置启动每一台mongod实例  
主要参数是 `mongod --replSet "rs0"`,replSet 参数指定 replica set的名字 , 也可以把配置放在配置文件中, 以下面的方式启动:
```
	mongod --config $HOME/.mongodb/config
```
1.  用mongo shell 连接到其中的一台mongo实例
```
	mongo --host 192.168.1.48 --port 27018
```
1. 初始化 replica set ,[rs.initiate()][4]  
```
	rs.initiate()
```
1. 验证初始化的配置, [rs.conf()][3]  
```
	rs.conf();

	// 输出
	{
		"_id" : "rs0",
		"version" : 1,
		"members" : [
			{
				"_id" : 0,
				"host" : "mdb2.xy.l99.com:27018"
			}
		]
	}
```
1. 把其它成员加入到 replica set, 用 [rs.add()][2]
```
rs.add('192.168.1.61:27018')
rs.add('192.168.1.64:27018')
// 添加完成后, 成员的stateStr会由 "UNKNOW" -> "STARTUP2" -> "SECONDARY"
```
```
// 1. 用mongo shell登录成员执行初始化 (这个不需要手动执行)
mongo --host 192.168.1.61 --port 27018
rs.initiate()
rs.status()    # 查看状态
```
执行后除了master两台的状态都是 `"stateStr" : "SECONDARY"`, SECONDARY上不能查询 .

# 错误

## replSet 参数不统一
```
// rs.add('192.168.1.61:27018') 时报错
{
	"errmsg" : "exception: set name does not match the set name host 192.168.1.61:27018 expects",
	"code" : 13145,
	"ok" : 0
}

```
## 数据错误

	// rs.add('192.168.1.61:27018') 时报错
	{
		"errmsg" : "exception: need most members up to reconfigure, not ok : 192.168.1.61:27018",
		"code" : 13144,
		"ok" : 0
	}

	 #启动时 --replSet参数值修改过会报这个错, 要清空 --datapath中数据重新启动

## SECONDARY不能查询
```
Sat May 31 16:33:53.904 error: { "$err" : "not master and slaveOk=false", "code" : 13435 } at src/mongo/shell/query.js:128

# 执行rs.slaveOk()后再查询
```

# 参考资料
[Deploy a Replica Set][1]  
[Remove Members from Replica Set][5]  




[1]: http://docs.mongodb.org/manual/tutorial/deploy-replica-set/  
[2]: http://docs.mongodb.org/manual/reference/method/rs.add/#rs.add
[3]: http://docs.mongodb.org/manual/reference/method/rs.conf/#rs.conf
[4]: http://docs.mongodb.org/manual/reference/method/rs.initiate/#rs.initiate
[5]: http://docs.mongodb.org/manual/tutorial/remove-replica-set-member/
