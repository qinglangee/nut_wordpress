# 创建第一个　chrome app

一个　Chrome App 包含以下部分：

* manifest　文件告诉　Chrome 你的 app 是什么　，　如何启动它以及它需要的额外权限．
* background　脚本用来创建事件响应页面管理 app 的生命同期．
* 代码必须包含在 Chrome App 包中．　包括　HTML, JS, CSS 和本地模块．
* 图标和其它资源也要包含在包中．

## 第一步，　创建　manifest
First create your manifest.json file (Formats: Manifest Files describes this manifest in detail):
首先新建一个 manifest.json 文件，　([Formats: Manifest Files][1] 描述了 manifest 的细节)

	{
	  "name": "Hello World!",
	  "description": "My first Chrome App.",
	  "version": "0.1",
	  "manifest_version": 2,
	  "app": {
	    "background": {
	      "scripts": ["background.js"]
	    }
	  },
	  "icons": { "16": "calculator-16.png", "128": "calculator-128.png" }
	}

*重要: Chrome Apps 必须使用 manifest version 2.*

## 第二步， 创建　background 脚本
新建一个 background.js

	chrome.app.runtime.onLaunched.addListener(function() {
	  chrome.app.window.create('window.html', {
	    'bounds': {
	      'width': 400,
	      'height': 500
	    }
	  });
	});

在上面的示例代码中，当 app 启动时 [onLaunched事件][2] 会被发出．　它会立即按指定的宽高打开一个窗口．　你的 background 脚本可以包含更多的 listener,window, post message and lauch data. 

## 第三步，　创建一个窗口页面
新建 window.html 

	<!DOCTYPE html>
	<html>
	  <head>
	  </head>
	  <body>
	    <div>Hello, world!</div>
	  </body>
	</html>
## 第四步，　创建图标
把这俩图标复制到你的 app 目录
[calculator-16.png][3]  
[calculator-128.png][4]  

## 启动你的 app

###　启用标志
很多 Chrome Apps APIs 还是实验性的，　所以你要打开实验　api 才可以用

* 打开 chrome://flags　页面.
* 找到 "Experimental Extension APIs", 点击 "Enable" 链接.
* 重启 Chrome.

### 加载 app
点击菜单图标，选择　_Tools > Extensions_, 打开应用和插件管理页面．　　
把　_Developer mode_　的多选框选上．　　
点击　_Load unpacked extension_ 打开你 app 的目录　．

### 或者, 从命令行加载和启动 app 
These command line options to Chrome may help you iterate:

`--load-and-launch-app=/path/to/app/` installs the unpacked application from the given path, and launches it. If the application is already running it is reloaded with the updated content.
`--app-id=ajjhbohkjpincjgiieeomimlgnll` launches an app already loaded into Chrome. It does not restart any previously running app, but it does launch the new app with any updated content.


# 另外一个更完整的多步骤的例子
[Build a Todo Chrome App](https://developer.chrome.com/apps/app_codelab_intro)  


refs:  
[Create Your First App](https://developer.chrome.com/apps/first_app)  



[1]: https://developer.chrome.com/apps/manifest
[2]: https://developer.chrome.com/apps/app_lifecycle#lifecycle
[3]: https://developer.chrome.com/static/images/calculator-16.png
[4]: https://developer.chrome.com/static/images/calculator-128.png