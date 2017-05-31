# javascript uri 编码



js 对文字进行编码涉及3个函数：*escape, encodeURI, encodeURIComponent*，相应3个解码函数：*unescape, decodeURI, decodeURIComponent*

1、   传递参数时需要使用encodeURIComponent，这样组合的url才不会被#等特殊字符截断。                            

例如：

	<script language="javascript">document.write('<a href="http://passport.baidu.com/?logout&aid=7& u='+encodeURIComponent("http://cang.baidu.com/bruce42")+'">退出</a& gt;');</script>

2、   进行url跳转时可以整体使用encodeURI
例如：

	Location.href="/encodeURI"("http://cang.baidu.com/do/s?word=百度&ct=21");

3、   js使用数据时可以使用escape

例如：搜藏中history纪录。

4、   escape对0-255以外的unicode值进行编码时输出 %uxxxx 格式，其它情况下escape，encodeURI，encodeURIComponent编码结果相同。


最多使用的应为encodeURIComponent，它是将中文、韩文等特殊字符转换成utf-8格式的url编码，所以如果给后台传递参数需要使用encodeURIComponent时需要后台解码对utf-8支持（form中的编码方式和当前页面编码方式相同）

escape 不编码字符有69个：*，+，-，.，/，@，_，0-9，a-z，A-Z

encodeURI 不编码字符有82个：!，#，$，&，'，(，)，*，+，,，-，.，/，:，;，=，?，@，_，~，0-9，a-z，A-Z

encodeURIComponent 不编码字符有71个：!， '，(，)，*，-，.，_，~，0-9，a-z，A-Z

 

 

根据说明 我需要的是encodeURIComponent函数

--------------------------------------------------------------------------------------------------------------

据上所述
1、浏览器，表单发的URL是和页面编码一致的
2、浏览器中用XMLHTTP发送的URL是和浏览器默认设置一致的
3、请求 URL 与服务器一致则无乱码出现

 

PS:  推荐使用 encodeURIComponent(), 用它编码过的 URL 与 PHP urlencode() 函数执行结果一致,交互最为便捷.




[js urlencode , encodeURIComponent](http://www.blogjava.net/freeman1984/archive/2010/06/07/322965.html)   