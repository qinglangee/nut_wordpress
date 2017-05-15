# 数据备份和恢复

## mongodump 

	// 导出数据
	mongodump -h 192.168.1.123 --port 12345 -d dbname -o /tmp/mongo_data
	// 恢复/导入数据
	mongorestore -h dbhost -d dbname --directoryperdb /tmp/mongo_data/dbname

	-h：MongoDB所在服务器地址

	-d：需要恢复的数据库实例，例如：dbname，当然这个名称也可以和备份时候的不一样，比如test2

	--directoryperdb：备份数据所在位置，例如：/tmp/mongo_data/dbname，这里为什么要多加一个dbname，而不是备份时候的mongo_data，读者自己查看提示吧！

	--drop：恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！

