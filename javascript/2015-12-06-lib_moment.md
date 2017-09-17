# 时间库 moment

## 当前日期、时间

	moment().format()  // 2015-12-06T13:03:42+08:00
	moment().format('YYYY-MM-DD')  // 2015-12-06
	moment().format('YYYY-MM-DD HH:mm:ss') // 2015-12-06 13:08:14
## 解析日期时间
```
var time = moment("2017-08-04 17:48", "YYYY-MM-DD HH:mm");
// 转换成date类型
date = time.toDate();
// Date 转换成 moment
myMoment = moment(date);
```

## 加减日期

	var now = moment();
	now.add(2,"d")      // 加两天
	now.add(2,"days")   // 加两天
	now.subtract(-2, "d")  // 加两天（减负数也是加）

	Key	Shorthand
	years	    y
	quarters	Q
	months	    M
	weeks   	w
	days	    d
	hours   	h
	minutes	    m
	seconds	    s
	milliseconds	ms
## 日期相减



更多示例参照[官方文档][1]  

refs:  
[moment doc]

[1](http://momentjs.com/docs/)  