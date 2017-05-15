# jquery ajax 
直接发送 ajax 请求， async为true 是异步请求， false 是同步请求。

	$.ajax({
        url : 'your url',
        data:{name:value},
        cache : false,
        async : false,
        type : "POST",
        dataType : 'json/xml/html',
        success : function (result){
            do something....
        }
    });

    var url = "http://www.baidu.com";
    var data = {"param1":123, "param2":456};
    var type = "json"; //  text  json  xml ...
    $.get(url, data, function(response){
    	console.log(response);
    }, type);