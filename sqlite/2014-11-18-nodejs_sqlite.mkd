# nodejs 使用 sqlite

## 快速启动示例
安装 [node-sqlite3][1],  就可以用了

	npm install sqlite3
示例代码,  API查询 [node-sqlite3 api][2]  

	var sqlite3 = require('sqlite3').verbose();
	var db = new sqlite3.Database(':memory:');   // 创建 内存数据库

	// 创建文件数据库
	//    var db = new sqlite3.Database('1.db');   //  相对路径
	//    var db = new sqlite3.Database('/tmp/1.db', function(){......});   //  绝对路径

	db.serialize(function() {
	  db.run("CREATE TABLE lorem (info TEXT)");

	  var stmt = db.prepare("INSERT INTO lorem VALUES (?)");
	  for (var i = 0; i < 10; i++) {
	      stmt.run("Ipsum " + i);
	  }
	  stmt.finalize();

	  db.each("SELECT rowid AS id, info FROM lorem", function(err, row) {
	      console.log(row.id + ": " + row.info);
	  });
	});

	db.close();

## 并行与串行模式
node-sqlite3 有两个函数来控制查询执行顺序, 默认是并行模式.

###    Database#serialize([callback])
在  serialize callback中一次只有一个statement执行一个查询, 完成之后其它的才能执行. callback执行完成后, 回到原来的模式. 
嵌套调用 serialize 是安全的.
不是*直接*放在 serialize callback中的查询就不是串行的.

	db.serialize(function() {
	    // These two queries will run sequentially.
	    db.run("CREATE TABLE foo (num)");
	    db.run("INSERT INTO foo VALUES (?)", 1, function() {
	        // 下面两句是并行执行, 第二句可能会报错, 因为表 bar 可能还没创建成功.
	        db.run("CREATE TABLE bar (num)");
	        db.run("INSERT INTO bar VALUES (?)", 1);
	    });
	});
如果直接调用 Database#serialize() 没有callback, 那么后面所有查询都是串行, 直到显式调用 Database#parallelize .
###    Database#parallelize([callback])
与 serialize 类似啦. 


## api

* new sqlite3.Database(filename, [mode], [callback])
* sqlite3.verbose()
* Database#  close([callback])
* Database#  run(sql, [param, ...], [callback])
* Database#  get(sql, [param, ...], [callback])
* Database#  all(sql, [param, ...], [callback])
* Database#  each(sql, [param, ...], [callback], [complete])
* Database#  exec(sql, [callback])
* Database#  prepare(sql, [param, ...], [callback])

* Statement#  bind([param, ...], [callback])
* Statement#  reset([callback])
* Statement#  finalize([callback])
* Statement#  run([param, ...], [callback])
* Statement#  get([param, ...], [callback])
* Statement#  all([param, ...], [callback])
* Statement#  each([param, ...], [callback], [complete])
* 
* 








refs:  
[node-sqlite3][1]  
[node-sqlite3 api][2]  


[1]: https://github.com/mapbox/node-sqlite3#installing  
[2]: https://github.com/mapbox/node-sqlite3/wiki/API  