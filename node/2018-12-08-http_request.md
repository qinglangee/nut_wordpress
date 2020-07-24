# node 发送 http 请求
http 模块和 request 模块  
http 是nodejs 自带的模块,直接能用. 包含server端和client端的支持  
[request][1] 是包装http的第三方模块, 需要安装使用, 用来简化http client端的开发.  

http模块提供了两个函数 http.request和 http.get，功能是作为客户端向http服务器发起请求。

## http.request(options,callback)
options是一个类似关联数组的对象，表示请求的参数，callback作为回调函数，需要传递一个参数，为http.ClientResponse的实例，http.request返回一个http.ClientRequest的实例。

options常用的参数有host、port（默认为80）、method（默认为GET）、path（请求的相对于根的路径，默认是“/”，其中querystring应该包含在其中，例如/search?query=byvoid）、headers（请求头内容）
var http=require("http");
```
var options={
    hostname:"cn.bing.com",
    port:8080
}

var req=http.request(options,function(res){
    res.setEncoding("utf-8");
    res.on("data",function(chunk){
        console.log(chunk.toString())
    });
    console.log(res.statusCode);
});
req.on("error",function(err){
    console.log(err.message);
});
req.end();
```
发送POST请求（模拟了向慕课网发起评论的功能，headers请使用开发者工具从请求中获取,基本上是参考scott老师的代码）
```
var http=require("http");
var querystring=require("querystring");

var postData=querystring.stringify({
    "content":"just a test",
    "mid":8837
});

var options={
    hostname:"www.imooc.com",
    port:80,
    path:"/course/document",
    method:"POST",
    headers:{
        "Accept":"application/json, text/javascript, */*; q=0.01",
        ......
        "X-Requested-With":"XMLHttpRequest",
    }
}

var req=http.request(options,function(res){
    res.on("data",function(chunk){
        console.log(chunk);
    });
    res.on("end",function(){
        console.log("### end ##");
    });
    console.log(res.statusCode);
});

req.on("error",function(err){
    console.log(err.message);
})
req.write(postData);
req.end();

```
## http.get(options,callback)
这个方法是http.request方法的简化版，唯一的区别是http.get自动将请求方法设为了GET请求，同时不需要手动调用req.end()，但是需要记住的是，如果我们使用http.request方法时没有调用end方法，服务器将不会收到信息。

## request
可以将request模块想象成一个简化版的第三方类http模块，同时支持https 和重定向，戳这里区官网。下文列出几个能够让你快速上手的知识点。

GET
```
request(url,function(error,response,body){
    if(!error && response.statusCode == 200){
        //输出返回的内容
        console.log(body);
    }
});
```
POST
```
var options = { 
  uri: 'https://www.googleapis.com/urlshortener/v1/url', 
  method: 'POST', 
  json: { "longUrl": "http://www.google.com/" }
};

request(options, function(error, response, body) {
    if (!error && response.statusCode == 200) {
        //输出返回的内容
        console.log(body);
    }
});

```
流  
任何响应都可以输出到文件流。  
`request('http://google.com/doodle.png').pipe(fs.createWriteStream('doodle.png'))`  
反过来，也可以将文件传给PUT或POST请求。未提供header的情况下，会检测文件后缀名，在PUT请求中设置相应的content-type。  
`fs.createReadStream('file.json').pipe(request.put('http://mysite.com/obj.json'))`  

表单  
request支持 application/x-www-form-urlencoded 和 multipart/form-data 实现表单上传。   
x-www-form-urlencoded：  
```
      request.post('http://service.com/upload', {form:{key:'value'}})
      或者：
      request.post('http://service.com/upload').form({key:'value'})
```
multipart/form-data
```
      var r = request.post('http://service.com/upload')
      var form = r.form()
      form.append('my_field', 'my_value')
      form.append('my_buffer', new Buffer([1, 2, 3]))
      form.append('my_file', fs.createReadStream(path.join(__dirname, 'doodle.png'))
      form.append('remote_file', request('http://google.com/doodle.png'))
```
```
var formData = { 
    // Pass a simple key-value pair 
    my_field: 'my_value', 
    // Pass data via Buffers 
    my_buffer: new Buffer([1, 2, 3]), 
    // Pass data via Streams 
    my_file: fs.createReadStream(__dirname + '/unicycle.jpg'), 
}; 
request.post({url:'http://service.com/upload', formData: formData}, function (error, response, body) { 
    if (!error && response.statusCode == 200) { 
    } 
})

```

## 服务器端接收文件
使用 [multiparty][2] 模块  
parse 之后默认把文件保存在了服务器上.  不想直接保存的时候关注一下part事件  
```
var multiparty = require('multiparty');
var http = require('http');
var util = require('util');
 
http.createServer(function(req, res) {
  if (req.url === '/upload' && req.method === 'POST') {
    // parse a file upload
    var form = new multiparty.Form();
 
    form.parse(req, function(err, fields, files) {
      res.writeHead(200, {'content-type': 'text/plain'});
      res.write('received upload:\n\n');
      res.end(util.inspect({fields: fields, files: files}));
    });
 
    return;
  }
 
  // show a file upload form
  res.writeHead(200, {'content-type': 'text/html'});
  res.end(
    '<form action="/upload" enctype="multipart/form-data" method="post">'+
    '<input type="text" name="title"><br>'+
    '<input type="file" name="upload" multiple="multiple"><br>'+
    '<input type="submit" value="Upload">'+
    '</form>'
  );
}).listen(8080);
```
fields 和 files数据结构, path是上传后保存的临时文件
```
fileds:   { title: [ '' ] }
files:    { upload: 
           [ { fieldName: 'upload',
               originalFilename: 'wood2.jpg',
               path: '/tmp/cq0cjaZESEl6m2vmtF8d5JQG.jpg',
               headers: [Object],
               size: 271227 } ] }

```

refs:  
[nodejs http模块的讲解以及request包的使用](https://blog.csdn.net/itkingone/article/details/79259490)  

[1]: https://github.com/request/request
[2]: https://www.npmjs.com/package/multiparty