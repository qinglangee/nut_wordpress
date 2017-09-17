# mongo date 查询

查询创建时间大于2017-06-24的记录
`db.data.find({create_at:{$gt:new Date("2017-5-24")}}, {create_at:1})`
`db.data.find({create_at:{$gt:ISODate("2017-05-23T16:10:38.576Z")}}, {create_at:1})`
*mongodb 存储时间是对应时区为0的,在不同的时区要注意时区的影响*

手动更新时间 (时间的数字必须是两位，不足的用0补齐)
`db.data.update({top:1},{$set:{create_at:new Date("2017-08-23T12:12:12.234567Z")}})`


根据日期排序
`db.data.find({post_type:10100}).sort({create_at:1})`