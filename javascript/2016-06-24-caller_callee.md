# js 的 caller callee
Arguments

该对象代表正在执行的函数和调用它的函数的参数。

[function.]arguments[n]
参数function ：选项。当前正在执行的 Function 对象的名字。 n ：选项。要传递给 Function 对象的从0开始的参数值索引。 


caller

返回一个对函数的引用，该函数调用了当前函数。
functionName.caller
functionName 对象是所执行函数的名称。
说明
对于函数来说，caller 属性只有在函数执行时才有定义。如果函数是由顶层调用的，那么 caller 包含的就是 null 。如果在字符串上下文中使用 caller 属性，那么结果和 functionName.toString 一样，也就是说，显示的是函数的反编译文本。
下面的例子说明了 caller 属性的用法：

	// caller demo {
	function callerDemo() {
	    if (callerDemo.caller) {
	        var a= callerDemo.caller.toString();
	        alert(a);
	    } else {
	        alert("this is a top function");
	    }
	}
	function handleCaller() {
	    callerDemo();
	}

caller 也可以用  arguments.callee.caller


[function.]arguments.callee
可选项 function 参数是当前正在执行的 Function 对象的名称。

说明

callee 属性的初始值就是正被执行的 Function 对象。

callee 属性是 arguments 对象的一个成员，它表示对函数对象本身的引用，这有利于匿名

	//递归计算
	var sum = function(n){
		if (n <= 0)                       
			return 1;
		else
		    return n ＋arguments.callee(n - 1)
	}