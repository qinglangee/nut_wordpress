# nodejs 操作 mongodb

## 安装 mongodb 库

	npm install mongodb

## 示例
建立连接

	  var MongoClient = require('mongodb').MongoClient, format = require('util').format;
	 
	  MongoClient.connect('mongodb://127.0.0.1:27017/test', function(err, db) {
	    if(err) throw err;
	 
	    var collection = db.collection('test_insert');
	    // 这里就有各种操作
	    // ...
	    // ...
	  })
带用户名密码连mongodb
	 
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
插入一条记录

	    collection.insert({a:2}, function(err, docs) {
	      
	      collection.count(function(err, count) {
	        console.log(format("count = %s", count));
	      });
	 
	      // Locate all the entries using find 
	      collection.find().toArray(function(err, results) {
	        console.dir(results);
	        // Let's close the db 
	        db.close();
	      });
	    });
数据类型

	  // Fetch the library 
	  var mongo = require('mongodb');
	  // Create new instances of BSON types 
	  new mongo.Long(numberString)
	  new mongo.ObjectID(hexString)
	  new mongo.Timestamp()  // the actual unique number is generated on insert. 
	  new mongo.DBRef(collectionName, id, dbName)
	  new mongo.Binary(buffer)  // takes a string or Buffer 
	  new mongo.Code(code, [context])
	  new mongo.Symbol(string)
	  new mongo.MinKey()
	  new mongo.MaxKey()
	  new mongo.Double(number)  // Force double storage 
查找

	  var cursor = collection.find(query, [fields], options);
	  cursor.sort(fields).limit(n).skip(m).
	 
	  cursor.nextObject(function(err, doc) {});
	  cursor.each(function(err, doc) {});
	  cursor.toArray(function(err, docs) {});
	 
	  cursor.rewind()  // reset the cursor to its initial state. 
排序

	.limit(n).skip(m) to control paging.
	.sort(fields) Order by the given fields. There are several equivalent syntaxes:
	.sort({field1: -1, field2: 1}) descending by field1, then ascending by field2.
	.sort([['field1', 'desc'], ['field2', 'asc']]) same as above
	.sort([['field1', 'desc'], 'field2']) same as above
	.sort('field1') ascending by field1

更新  
Note that there's no reason to pass a callback to the insert or update commands unless you use the w:1 option. If you don't specify w:1, then your callback will be called immediately

    db.collection('test').update({hi: 'here'}, {$set: {hi: 'there'}}, {w:1}, function(err) {
      if (err) console.warn(err.message);
      else console.log('successfully updated');
    });
查找并更新

    db.collection('test').findAndModify({hello: 'world'}, [['_id','asc']], {$set: {hi: 'there'}}, {}, function(err, object) {
      if (err) console.warn(err.message);
      else console.dir(object);  // undefined if no matching object exists. 
    });
Save
The save method is a shorthand for upsert if the document contains an _id, or an insert if there is no _id.


refs:  
[API doc](http://mongodb.github.io/node-mongodb-native/)  
[API doc quick start](http://mongodb.github.io/node-mongodb-native/2.0/)