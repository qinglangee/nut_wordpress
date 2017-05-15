# Aggregation [聚合函数][1]

Aggregation 可以实现数据库的 `group by` 功能。

	db.web_user_match.aggregate([{$match:{gid:{$gt:0}}}, {$group:{_id:"$gid",total:{$sum:1}}}])
## 三种实现聚合的方式
MongoDB provides three ways to perform aggregation: the aggregation pipeline, the map-reduce function, and single purpose aggregation methods.

### aggregation pipeline 是推荐的方式， 在mongodb内部是用本地代码实现的。

orders表中符合 status=A的记录，对 cust_id 字段作group操作， 返回 amout 字段的和。
*返回结果有大小限制，不能超过16M, 中间处理结果不能超过100M*

	db.orders.aggregate([
		{$match: {status:"A"}},
		{$group: {_id:"$cust_id", total:{$sum:"$amount"}}}
	]);
### map-erduce 用js 功能实现map/reduce, 提供了更大的灵活性，但与 aggregation pipeline 相比效率低一些，也更复杂。
orders表中符合 status=A的记录，返回所有 amout 字段的和。这里就不能 group 了

	db.orders.mapReduce(
		function(){emit(this.cust_id,this.amount)},
		function(key,values){return Array.sum(values)},
		{
			query:{status:"A"},
			out:"order_totals"
		}
	)

### single purpose aggregation methods	
MongoDB also provides `db.collection.count()`, `db.collection.group()`, `db.collection.distinct()`. special purpose database commands.

	db.orders.distinct("cust_id")  -> [ "A123", "B212" ]
group()

根据`ord_dt` 和 `item.sku` 分组 `ord_dt` 大于 01/01/2011 的记录

	SELECT ord_dt, item_sku FROM orders WHERE ord_dt > '01/01/2012' GROUP BY ord_dt, item_sku

	db.orders.group(
	   {
	     key: { ord_dt: 1, 'item.sku': 1 },
	     cond: { ord_dt: { $gt: new Date( '01/01/2012' ) } },
	     reduce: function ( curr, result ) { },
	     initial: { }
	   }
	)

求和 

	SELECT ord_dt, item_sku, SUM(item_qty) as total FROM orders WHERE ord_dt > '01/01/2012' GROUP BY ord_dt, item_sku
	
	db.orders.group(
	   {
	     key: { ord_dt: 1, 'item.sku': 1 },
	     cond: { ord_dt: { $gt: new Date( '01/01/2012' ) } },
	     reduce: function( curr, result ) {
	                 result.total += curr.item.qty;
	             },
	     initial: { total : 0 }
	   }
	)
求平均值

	db.orders.group(
	   {
	     keyf: function(doc) {
	               return { day_of_week: doc.ord_dt.getDay() };
	           },
	     cond: { ord_dt: { $gt: new Date( '01/01/2012' ) } },
	    reduce: function( curr, result ) {
	                result.total += curr.item.qty;
	                result.count++;
	            },
	    initial: { total : 0, count: 0 },
	    finalize: function(result) {
	                  var weekdays = [
	                       "Sunday", "Monday", "Tuesday",
	                       "Wednesday", "Thursday",
	                       "Friday", "Saturday"
	                      ];
	                  result.day_of_week = weekdays[result.day_of_week];
	                  result.avg = Math.round(result.total / result.count);
	              }
	   }
	)
## aggregation pipeline
## map-reduce function
## single purpose aggregation methods.



[1]: https://docs.mongodb.org/manual/aggregation/
[2]: https://docs.mongodb.org/manual/reference/method/db.collection.group/#db.collection.group