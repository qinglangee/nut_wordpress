# mongo date 查询

查询创建时间大于2017-06-24的记录
`db.data.find({create_at:{$gt:new Date("2017-5-24")}}, {create_at:1})`
`db.data.find({create_at:{$gt:ISODate("2017-05-23T16:10:38.576Z")}}, {create_at:1})`
*mongodb 存储时间是对应时区为0的,在不同的时区要注意时区的影响*




根据日期排序
`db.data.find({post_type:10100}).sort({create_at:1})`