# js 函数示例

向上取整

	Math.ceil(3.2)  // 4
	Math.ceil(3)    // 3
	Math.ceil(-1.2) // -1
向下取整

	Math.floor(3.2)   // 3
	Math.floor(3)     // 3
	Math.floor(-1.2)  // -2
[其它Math函数][1]
解析整数

	parseInt("123")   // 123
	parseInt("abc")   // NaN
	parseInt("abc123")   // NaN
	parseInt("456abc123")   // 456
	parseInt("456.123")   // 456
字符串替换 [w3c  replace][4]

	var a = "ababcdababcd";
	var b = a.replace("ab", "mn"); // b= "mnabcdababcd"; 只替换第一个
	var c = a.replace(/ab/g, "mn"); // c= "mnmncdmnmncd"; 正则可以全局替换
	var d = a.replace(/ab/g, functiion(str){return str.length;}); // d = "22cd22cd";  可以用函数返回
字符串分割

	var lines = content.split('\n');
数组操作

splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目。[w3c splice][2]  
*注释：该方法会改变原始数组*
参数 	    描述
index 	    必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
howmany 	必需。要删除的项目数量。如果设置为 0，则不会删除项目。
item1, ..., itemX 	可选。向数组添加的新项目。

	arrayObject.splice(index,howmany,item1,.....,itemX)
slice() 截取数组的一部分 [w3c slice][3]  
start 	必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。
end 	可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。
返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素

	arrayObject.slice(start,end)
	var a = [1,2,3,4,5,6,7];
	var b = a.slice(3,2);  // b = [4,5]

随机数

	Math.random()  // 返回 0.0~1.0之间的伪随机数
	Math.floor(Math.random() * 10);

定时执行

	// interval
	var count=1;
	function exe(){
	  console.log(count++);
	}
	var timer = setInterval(exe, 1000);

	clearInterval(timer);

	// timeout
	var count=1;
	function exe(){
	  console.log(count++);
	  if(count < 5)
	  setTimeout(exe, 1000);
	}
	var timer = setTimeout(exe, 1000);

	// timeout 带参数

	function prt(i){
	  if(i > 4){return;}
	  console.log(i);
	  setTimeout(function(){prt(i+1)}, 1000);
	}
	prt(1);

数组操作
添加/删除 元素

	arrayObject.push(newelement1,newelement2,....,newelementX); // push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度。
	arrayObject.pop(); // pop() 方法用于删除并返回数组的最后一个元素。
	arrayObject.unshift(newelement1,newelement2,....,newelementX); // unshift() 方法可向数组的开头添加一个或更多元素，并返回新的长度。
	arrayObject.shift(); // shift() 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。

正则

    var a = /aa(\d+)cc/;
	var group = "aa77cc".match(a);
	if(group != null){
		for(var i=0;i<group.length;i++){
		  console.log("i is :" + i + " " + group[i]);
		}
	}
refs:  
[javascript Math 函数][1]  


[1]: http://www.w3school.com.cn/jsref/jsref_obj_math.asp
[2]: http://www.w3school.com.cn/jsref/jsref_splice.asp
[3]: http://w3school.com.cn/jsref/jsref_slice_array.asp
[4]: http://www.w3school.com.cn/jsref/jsref_replace.asp
