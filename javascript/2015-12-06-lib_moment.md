# 时间库 moment

当前日期、时间

	moment().format()  // 2015-12-06T13:03:42+08:00
	moment().format('YYYY-MM-DD')  // 2015-12-06
	moment().format('YYYY-MM-DD HH:mm:ss') // 2015-12-06 13:08:14
加减日期

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



更多示例参照[官方文档][1]  

refs:  
[moment doc]

[1](http://momentjs.com/docs/)  