# nodejs 文件操作相关

`var fs = requier 'fs'`
## 读文件

	fs.readFile('./json.json',function(err,data){
	    if(err) throw err;
	    var jsonObj = JSON.parse(data);
	});
## 写文件

	var fs = require('fs');
	fs.writeFile("./filename.txt", "file_content", function(err){
		if(err) throw err;
	});
## 判断文件是否存在

	// 已过时 Deprecated: Use fs.stat() or fs.access() instead.
	fs.exists('/etc/passwd', (exists) => {
	  console.log(exists ? 'it\'s there' : 'no passwd!');
	});
	// 已过时 Deprecated: Use fs.statSync() or fs.accessSync() instead.
	var exist = fs.existsSync(path); // 返回 true false
## 遍历目录
深度优先遍历

		var fs = require('fs'),  
		    fileList = [];

		function walk(path){  
		    var dirList = fs.readdirSync(path);
		    dirList.forEach(function(item){
		        if(fs.statSync(path + '/' + item).isDirectory()){
		            walk(path + '/' + item);
		        }else{
		            fileList.push(path + '/' + item);
		        }
		    });
		}

		walk('/dirName');

		console.log(fileList); 

广度优先遍历

		fileList = [];
		function walk(path){  
		    var dirList = fs.readdirSync(path);

		    dirList.forEach(function(item){
		        if(fs.statSync(path + '/' + item).isFile()){
		            fileList.push(path + '/' + item);
		        }
		    });

		    dirList.forEach(function(item){
		        if(fs.statSync(path + '/' + item).isDirectory()){
		            walk(path + '/' + item);
		        }
		    });
		}		

refs:  
[nodejs file system api](https://nodejs.org/api/fs.html)  
[nodejs目录遍历](https://swordair.com/directory-traversal-in-nodejs/)  
