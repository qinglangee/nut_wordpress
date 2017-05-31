# MongoDB Replication

## 介绍

### 目的
数据备份冗余, 防止单点挂机. 还可以提高读数据的承受能力.

### Replication in MongoDB
副本集合是一组有着相同数据的mongod实例, 其中一台作主要机, 其余的作次要机.
只在主要机接收写操作, 次要机从主要机中复制写操作.复制功能是异步执行的.

## replica set 成员
### Replica Set Primary
Primary 是唯一接受写操作的成员.   
所有成员都可以接受读操作, 默认配置下应用把读操作指向primary. 点 [Read Preference][2]查看如何修改默认行为有关的细节.
### Secondary成员
secondary 通过 [oplog][3] 冗余 primary的数据. 
secondary 成员可以被配置成不同的成员
### Non-voting 成员
在选举中不能投票, 但可以投反对票, 
### Priority 0 成员
这种成员不能选举成为 primary, 其它与secondary成员没有区别.   
在多数据中心的情况下, 可以只让一个中心的成员可以成为primary.
### Hidden 成员
Hidden成员维护一份primary数据的复本, 但对应用程序不可见, hidden成员必须是priority 0成员, db.isMaster()方法不显示hidden成员, 但hidden成员在选举中可以投票.  
In a sharded cluster, mongos do not interact with hidden members.  
在做数据备份时,可以用db.fsyncLock() 和 db.fsyncUnlock() 把所有写入刷新到磁盘, 并在备份操作期间锁定 mongod 实例, 这样就不需要在备份时停掉hidden成员.

#### 深入阅读
关于如何备份数据库, 看[MongoDB Backup Methods][4]. 如何配置一个hidden成员, 看 [Configure a Hidden Replica Set Member][5].

### Arbiter
只能用来进行选举, 在偶数台机器的 replica set 中加入 Arbiter, 奇数的不加.  
To add an arbiter, see [Add an Arbiter to Replica Set][6].

## 部署
[Deploy a Replica Set][1]

### 概览
三台机器的副本集可以
### 部署一个副本集
### 从replica set中删除一个成员

## replica set 成员配置

### 调整成员 proority



[1]: http://docs.mongodb.org/manual/tutorial/deploy-replica-set/
[2]: http://docs.mongodb.org/manual/core/read-preference/
[3]: http://docs.mongodb.org/manual/core/replica-set-oplog/
[4]: http://docs.mongodb.org/manual/core/backups/
[5]: http://docs.mongodb.org/manual/tutorial/configure-a-hidden-replica-set-member/
[6]: http://docs.mongodb.org/manual/tutorial/add-replica-set-arbiter/
