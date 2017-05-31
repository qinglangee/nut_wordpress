# soso地图的bug

如果加载这个版本的sosomap

	http://api.map.soso.com/v1.0/main.js?callback=mapEventHandler
那么页面中需要加入下面这个设置, 否则在高版本的IE中显示不出来. 其它版本的soso map 不清楚 

	<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7" />