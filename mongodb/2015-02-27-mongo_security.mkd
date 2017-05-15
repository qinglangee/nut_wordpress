# mongodb 安全配置

## 开启客户端访问控制

启动mongodb时设置 [authorization][1] 或 [keyFile][2] 来开启访问控制. authorization 用于单台实例, keyFile用于 replica set .  

1.用authorization的方式, 在 config文件中设置 auth

	auth=true
2.从localhost连接mongodb
3.创建管理用户  *2.6之前的用[db.addUser()][3], createUser是2.6版本才开始有的*  , 而且连接的客户端也要用2.6版本的

	use admin
	db.createUser(
		{
			user: "siteUserAdmin",
			pwd: "password",
			roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
		}
	)
也可以只创建单个数据库的管理员, 这们的只能管理这一个数据库. *要先use被管理的数据训, 否则创建了也连接不上*

	use records
	db.createUser(
		{
			user: "recordsUserAdmin",
			pwd: "password",
			roles: [ { role: "userAdmin", db: "records" } ]
		}
	)	
*在同一个数据库中(比如在admin中)不能创建用户名相同的两个用户(这不是废话吗), 在两个数据库中可以*
4.创建用户后, 本地连接上也不能查询, 必须有验证才行
5.向数据库中添加用户

	mongo  -u zhch -p  --authenticationDatabase admin    # 交互式输入密码
	mongo  -u zhch -p zhch --authenticationDatabase admin  

	use admin
	db.createUser(
	    {
	      user: "reportsUser",
	      pwd: "12345678",
	      roles: [
	         { role: "read", db: "reporting" },
	         { role: "read", db: "products" },
	         { role: "readWrite", db: "accounts" }
	      ]
	    }
	)
6.下面来看一下在nodejs中怎样带用户名密码连mongodb

	 
	  MongoClient.connect('mongodb://zhch:password@127.0.0.1:27017/admin', function(err, db) {
	    if(err) throw err;
	 
	 	// 先连接验证数据库, 连接后db切换到有权限查询的数据库
	    var collection = db.db("mydbname").collection('test_insert');
	  })

	  // 另一种是直接在目标数据库中建立用户数据(就是userAdmin类型的), 就可以直接连接了
	  MongoClient.connect('mongodb://zhch:password@127.0.0.1:27017/web', function(err, db) {
	    if(err) throw err;
	 
	 	// 先连接验证数据库, 连接后db切换到有权限查询的数据库
	    var collection = db.collection('test_insert');
	  })


##  查看所有的用户信息

	use admin
	db.system.users.find();
refs:  

[mongodb 开启访问控制](http://docs.mongodb.org/manual/tutorial/enable-authentication/)  
[向数据库中添加一个用户](http://docs.mongodb.org/manual/tutorial/add-user-to-database/)  



[1]: http://docs.mongodb.org/manual/reference/configuration-options/#security.authorization 
[2]: http://docs.mongodb.org/manual/reference/configuration-options/#security.keyFile
[3]: http://docs.mongodb.org/manual/reference/method/db.addUser/