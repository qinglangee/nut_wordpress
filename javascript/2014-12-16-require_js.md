# require js 日常

## 导入requirejs

如果目录结构是这样

* project-directory/
** project.html
** scripts/
*** main.js
*** require.js
*** helper/
**** util.js

导入代码是这样:

	<script data-main="scripts/main" src="scripts/require.js"></script>
也可以写绝对路径

	<script type="text/javascript" data-main="<%=path.static%>/js/index.js" src="<%=path.static%>/js/require.js" ></script>
其它的依赖关系在main.js中写了, 这样保证只有一个入口 

	require(["helper/util"], function(util) {
	    //This function is called when scripts/helper/util.js is loaded.
	    //If util.js calls define(), then this function is not fired until
	    //util's dependencies have loaded, and the util argument will hold
	    //the module value for "helper/util".
	});
*就O了*


## 文档摘录

### 加载 javascript 文件
requirejs 加载相对于 baseUrl的文件, baseUrl默认就是data-main属性中文件的目录. 当然也可以在[配置][1]中设置. 都没有的话就是html所在的目录.

加载时的module IDs会被转换成 baseUrl + path 的形式, 自动加上.js后缀.*以下几种情况例外* :

1. Ends in ".js".
2. Starts with a "/".
3. Contains an URL protocol, like "http:" or "https:".

配置浏览器全局的script, 可以用 [shim config][2], 这个略麻烦, 就不看了. 

*require js modules可以有以下几咎类型*
键值对,   就是键值对, 简单明了

	define({
	    color: "black",
	    size: "unisize"
	});
如果不需要依赖其它模块, 直接就一个函数

	define(function () {
	    //Do setup work here

	    return {
	        color: "black",
	        size: "unisize"
	    }
	});
普通需要依赖的

	//my/shirt.js now has some dependencies, a cart and inventory
	//module in the same directory as shirt.js
	define(["./cart", "./inventory"], function(cart, inventory) {
	        //return an object to define the "my/shirt" module.
	        return {
	            color: "blue",
	            size: "large",
	            addToCart: function() {
	                inventory.decrement(this);
	                cart.add(this);
	            }
	        }
	    }
	);
module直接就是一个函数

	define(["my/cart", "my/inventory"],
	    function(cart, inventory) {
	        //return a function to define "foo/title".
	        //It gets or sets the window title.
	        return function(title) {
	            return title ? (window.title = title) :
	                   inventory.storeName + ' ' + cart.name;
	        }
	    }
	);

关于获取相对路径的modules

	define(["require", "./relative/name"], function(require) {
	    var mod = require("./relative/name");
	});
a b 循环依赖

	//Inside b.js:
	define(["require", "a"],
	    function(require, a) {
	        //"a" in this case will be null if "a" also asked for "b",
	        //a circular dependency.
	        return function(title) {
	            return require("a").doSomething();
	        }
	    }
	);
调用 JSONP

	require(["http://example.com/api/data.json?callback=define"],
	    function (data) {
	        //The data object will be the API response for the
	        //JSONP data call.
	        console.log(data);
	    }
	);

refs:

[require js api 文档](http://requirejs.org/docs/api.html)  



[1]: http://requirejs.org/docs/api.html#config  
[2]: http://requirejs.org/docs/api.html#config-shim
	